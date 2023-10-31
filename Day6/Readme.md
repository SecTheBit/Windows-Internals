# Process and Jobs

### Process Environment Block
- The PEB is a structure which holds data about the current process under it’s field values – some fields being structures themselves to hold even more data.
- It contains information about a “running” process like: the process name, PID and loaded modules.
- Moreover, we can access the PEB structure from user-mode
- Let's See the PEB structure
```
  typedef struct _PEB {
  BYTE                          Reserved1[2];
  BYTE                          BeingDebugged;
  BYTE                          Reserved2[1];
  PVOID                         Reserved3[2];
  PPEB_LDR_DATA                 Ldr;
  PRTL_USER_PROCESS_PARAMETERS  ProcessParameters;
  PVOID                         Reserved4[3];
  PVOID                         AtlThunkSListPtr;
  PVOID                         Reserved5;
  ULONG                         Reserved6;
  PVOID                         Reserved7;
  ULONG                         Reserved8;
  ULONG                         AtlThunkSListPtr32;
  PVOID                         Reserved9[45];
  BYTE                          Reserved10[96];
  PPS_POST_PROCESS_INIT_ROUTINE PostProcessInitRoutine;
  BYTE                          Reserved11[128];
  PVOID                         Reserved12[1];
  ULONG                         SessionId;
} PEB, *PPEB;
```


The PEB Structure contains the following elements
1. Reserved1[2] : Reserved for internal use by the operating system.
2. Reserved3[2] : Reserved for internal use by operating system.
3. Ldr : Pointer to PEB_LDR_DATA structure that contains information about the loaded modules for the process.
4. Process Parameters: A pointer to an RTL_USER_PROCESS_PARAMETERS structure that contains process parameter information such as the command line
5. All the other elements are reserved for internal purpose only. Refer here https://learn.microsoft.com/en-us/windows/win32/api/winternl/ns-winternl-peb

### Image Loader
- A loader is a type of program that is responsible for loading programs and libraries into memory,and linking together all the necessary dependencies to run an application
- when a process is started on the system, the kernel creates a process object to represent it and performs various kernel-related initialization tasks, these tasks are performed by the image loader.
- The image loader lives in the user-mode system DLL Ntdll.dll and not in the kernel library. Therefore, it behaves just like standard code that is part of a DLL, and it is subject to the same restrictions in terms of memory access and security rights.
- The image loader will always be present in the running process


## Jobs
- Jobs function is to control one or more than one process called as group.
- A job object’s basic function is to allow groups of processes to be managed and manipulated as a unit.
- A job object is created using the ```CreateJobObject``` API
  
