### Virtual Memory
- This concept of virtual memory is helpful when a page (small chunk of memory, having default size of 4kb) wants to be loaded into the memory(secondary) but memory is not available, then in that particular scenario virtual memory comes into picture and allows some memory from RAM itself.
- Virtual Memory is a storage scheme that provides user an illusion of having a very big main memory. This is done by treating a part of secondary memory as the main memory.
- Read more about working of virtual memory here https://www.techtarget.com/searchstorage/definition/virtual-memory#:~:text=A%20system%20using%20virtual%20memory,having%20to%20purchase%20more%20RAM.
- We will se more about Virtual memory working, translation of address in upcoming days.

Note: A page, memory page, or virtual page is a fixed-length contiguous block of virtual memory, described by a single entry in the page table. It is the smallest unit of data for memory management in a virtual memory operating system.

  ### Kernel Mode vs User Mode

  #### Introduction
  - User application code runs in user mode, whereas OS code (such as system services and device drivers) runs in kernel mode.
  - Kernel mode refers to a mode of execution in a processor that grants access to all system memory and all CPU instructions.
  - These privilege levels or modes is called as rings.
  - When you open a process in user mode , the os createas a private virtual space because os wants to isolate the application's process from other process, so if a process crashes , it doesn't affect the other process.
    Whereas the kernel mode isn't isolated from the other drivers and the OS itself, so if a kernel driver crashes whole OS will crash
![POC](https://github.com/SecTheBit/Windows-Internals/assets/46895441/eaecc6a4-4e44-445a-ae64-71cf4b142413)

#### Ring
![POC](https://github.com/SecTheBit/Windows-Internals/assets/46895441/73575372-a6c6-4a3e-bb47-dfa6d71c6993)
- Kernel mode operates in ring 0 level, where it have access to all memory regions and CPU
- Every applications running in normal user context will work in ring 3 level.
- The OS uses ring 1 to interact with the computer’s hardware. This ring would need to run commands such as streaming a video through a camera on our monitor. Instructions that must interact with the system storage, loading, or saving files are stored in ring 2.

#### Memory Regions
- Pages in kernel/system mode space can be accessible from system itself not from user mode.
- Pages in user mode space can be accessible from both user and kernel mode
- Page which are not writable (only redable) cannot be writable from any mode
- Additionally, on processors that support no-execute memory protection, Windows marks pages containing data as non-executable, thus preventing inadvertent or malicious code execution in data 
  areas (if this feature, Data Execution Prevention [DEP] is enabled
- Windows doesn’t provide any protection for private read/write system memory being used by components running in kernel mode. In other words, once in kernel mode, OS and device-driver code 
  has complete access to system-space memory and can bypass Windows security to access objects.
- This lack of protection also emphasizes the need to remain vigilant when loading a third-party device driver, especially if it’s unsigned, because once in kernel mode, the driver has 
  complete access to all OS data

#### Driver signing
- If someone loads a malicious driver in kernel mode, then the attacker have access to all memory region and CPU which is not good from a security perspective.
- Keeping the security in mind, microsoft introduces a siginificant approach to deal with the problem, which is basically signing the drivers from legitimate authorities.
- For windows 10, all the kernel drivers must be signed by the two of the accepted certification authorities with SHA1 Extended Validation(EV) Hardware certificate, and once the driver is signed, it must be submitted to microsoft through System Device (SysDev) portal for attestaion signing. This step ensures that drives receives one more signature from microsoft.
- On top of the aforementioned EV requirements, mere attestation signing is insufficient. For a Windows 10 driver to load on a server system, it must pass through stringent Windows Hardware Quality Labs (WHQL) certification as part of the Hardware Compatibility Kit (HCK) and be submitted for formal evaluation, then only driver can be loaded into kernel mode.
- This is how microsoft protects the OS from malicious drivers.

#### Context Switch
- When a user level application wants to perform an action which is only possible in kernel mode like accessing hardware, modifying system settings, then it make syscalls to kernel which helps in doing such operations. 
- This switching between user mode to kernel mode called as Context switching
- Mode switching can be time-consuming and resource-intensive, and can impact system performance
- Modern operating systems use various techniques to minimize mode switching, such as caching kernel mode data in user mode, and using hardware support for virtualization and context 
  switching.
- Read more in depth https://www.geeksforgeeks.org/user-mode-and-kernel-mode-switching/

### Windows Registry
- It is a database that contains all information needed to boot and configure the system, system-wide software settings that control operation of windows , the security database and user settings and configurtions.
- It also contains information about current harware settings, loaded device drivers , resources being used by device drivers,etc.
- Registry keys are containers that act like folders, with values or subkeys contained within them.
- The main branches of the registry are called hives. And most PCs have five of them. All the folders in the registry are called keys except for these five hives
  - HKEY_CLASSES_ROOT
  - HKEY_CURRENT_USER
  - HKEY_LOCAL_MACHINE
  - HKEY_USERS
  - HKEY_CURRENT_CONFIG
- Inside these hives are more folders called keys. Keys contain values, which are the settings themselves.
- Reference https://www.avast.com/c-windows-registry

 
