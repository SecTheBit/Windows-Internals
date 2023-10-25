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

### 
