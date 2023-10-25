# Concept and Tools

## Windows API Flavours

### Windows API

- Windows appplication programming Interface is the user mode system programming interface to windows OS family.
- All the older API is written in C/C++
- C was chosen because it was that low enogh that can easily interact with OS Services

### OLE
- Object Linking and Embedding enables microsoft office applications to communicate and exchange data between documents(such as inserting an excel chart into mirosoft document)
- OLE is based on DDE, Dynamic Data Exchange , which is an older method of data exchanging
- DDE have some limitiation and secuity issues which have given rise to COM. Read here https://revelate.co/blog/dynamic-data-exchange/

### Component Object Model
- It helps in data excahnge using Interfaces, that we called as Windows API
- The APIs can be easily called from any language like C, C++, Visual Baic, etc.

### Windows RunTime
 - The Windows Runtime (WinRT) is the technology that powers the Universal Windows Platform, letting developers write applications that are common to all Windows devices, from Xbox to PCs to HoloLens to phones.
 - WinRT APIs are easily accessible from managed languages like C#, however for native C++ developers, using WinRT either requires a lot of complex COM code, or the use of Visual C++ component extensions, better known as C++/CX
 - Read Here https://blogs.windows.com/windowsdeveloper/2016/11/28/standard-c-windows-runtime-cwinrt/

## Services, Functions and routines

### Process
- Process is a container for a set of resources used when executing the instance of the program
- Process conains following things
  - Virtual Space : Set of virtual memory space that a process can used.
  - Executable Program : EXE
  - Open Handles : List of open handles of objects like semaphores,files,etc. that can be used by a process
  - Security Context: Basically an Access token which can specify what can be accessed by a process
  - process id: ID of the process
  - Atleast One thread

#### Process Status
- Status column will specify , what is the status of a process. It could be Running, Suspended, Not Responding
- Running (Non UI) : If a process do not have UI , then Running means that the process is waiting for some kernel object being signaled or some I/O operation to complete
- Running (UI) : If a process have a UI, then it means that it is waiting for some UI Input
- Suspended : If a process loses its foreground UI (or user clicks on minimize option), then it goes into suspended state so that battery/power can be saved.
- Not Responding : The process (actually the thread that owns the window) may be busy doing some CPU-intensive work or waiting on something else entirely.


### Threads
- It is just an entity in a process
- A process can have multiple threads
- A process in independeent of other process running in the system, whereas threads are interdependent to each other
- Theads shared memory with each other within a process, whereas process do not share memory with other processes.
- By default, threads don’t have their own access token, but they can obtain one, thus allowing individual threads to impersonate the security context of another process—including processes 
  on a remote Windows system—without affecting other threads in the process
- A thread contain following things:
  - Content of CPU registers representing the state of processor
  - Two stacks , one for execution in kernel level, and one for execution in user mode.
  - TLS : Thread local storage , used by DLLs, runtime libraies, etc.
  - Thread ID : Unique ID of a thread
  - Red here more about process and threads : https://de-engineer.github.io/Processes-threads-jobs-fibers/
 
#### Thread Scheduling
- They provide developers with the ability to implement custom scheduling algorithms that suit the specific needs of their applications.
- Fibers and UMS are two types of thread scheduling mechanism.

### Jobs
- Jobs function is to manage and manipulate groups of processess as unit.




