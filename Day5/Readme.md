## Process and Jobs

### Creating a Process

- CreateProcess is one of the functions provided by the Windows API which can helps in creating process
- If above function gets called , then it will call a internal function CreateProcessInternal, which will helps in calling NtCreateUserProcess in ntdll.dll in kernel mode,which will continue the kernel-mode part of process creation in the function with the same name
- ![image](https://github.com/SecTheBit/Windows-Internals/assets/46895441/c9dbf4d3-0739-46ca-bcad-7bfd228578fe)

### CreateProcess Function Explained
```
BOOL CreateProcessA(
  [in, optional]      LPCSTR                lpApplicationName,
  [in, out, optional] LPSTR                 lpCommandLine,
  [in, optional]      LPSECURITY_ATTRIBUTES lpProcessAttributes,
  [in, optional]      LPSECURITY_ATTRIBUTES lpThreadAttributes,
  [in]                BOOL                  bInheritHandles,
  [in]                DWORD                 dwCreationFlags,
  [in, optional]      LPVOID                lpEnvironment,
  [in, optional]      LPCSTR                lpCurrentDirectory,
  [in]                LPSTARTUPINFOA        lpStartupInfo,
  [out]               LPPROCESS_INFORMATION lpProcessInformation
);
```
- If you see above , there are several parameters which are required while calling CreateProcess functions, let's understand one by one:
  - lpApplicationName: The name of the application (exe, dll) to be executed
  - lpCommandLine: Any optional command line arguments to fire with the application.
  - lpProcesAttributes: Pointer to SECURITY_ATTRIBUTES structure which will determine whether the newly created process can be inherited or not. I always Use NULL for this parameter
  - lpThreadAttributes: Pointer to SECURITY_ATTRIBUTES structure which will determine whether the newly created thread object can be inherited or not.
  - bInheritHandles: If this parameter is TRUE, each inheritable handle in the calling process is inherited by the new process.
  - dwCreationFlags: Process creation flags, refer here https://learn.microsoft.com/en-us/windows/win32/procthread/process-creation-flags
  - lpEnvironment: A pointer to the environment block for the new process. If this parameter is NULL, the new process uses the environment of the calling process.
  - lpStartupInfo: Pointer to STARTUPINFOEX structure
  - lpProcessInformation: A pointer to a PROCESS_INFORMATION structure that receives identification information about the new process.
 
- If you worried about unknown data types used above, refer here: https://learn.microsoft.com/en-us/windows/win32/winprog/windows-data-types

