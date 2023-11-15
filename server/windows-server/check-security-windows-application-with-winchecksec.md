# 👺 Check Security Windows Application with Winchecksec

{% hint style="info" %}
Winchecksec เป็น Open Source Security Framework ของทางฝั่ง Windows Application ที่ใช้ในการตรวจสอบความปลอดภัยของโปรแกรม อย่างการที่แฮกเกอร์สามารถนำโค้ดไปแทรกรันบนโปรแกรม แล้วทำการเรียก System Call ซึ่งโดยปกติจะมี Address ที่ตายตัว แต่หากทำการ Random Address ด้วยเทคนิค ASLR ก็จะสามารถเพิ่มความปลอดภัยให้กับโปรแกรม
{% endhint %}

## **✨ Feature**

* Address-Space Layout Randomization ( ASLR ) & High-Entropy ASLR ( HEASLR )
* Authentication & Integrity Protection
* Data Execution Prevention ( DEP )
* Manifest Isolation
* Structured Exception Handling ( SEH ) and SafeSEH
* Control Flow Guard ( CFG ) and Return Flow Guard ( RFG )
* Guard Stack ( GS )

## **✅ Requirement**

* [Install CMake](https://cmake.org/download/)
* [Install Visual Studio 2017](https://docs.microsoft.com/en-us/visualstudio/releasenotes/vs2017-relnotes)

## **🏆 Get Started**

* ทำการดาวน์โหลด Winchecksec จาก GitHubgit clone --recurse -submodules https://github.com/trailofbits/winchecksec.git

{% code title="C:\>" %}
```
cd winchecksec
```
{% endcode %}

* ทำการสร้างโฟลเดอร์ build

{% code title="C:\winchecksec>" %}
```
mkdir build
```
{% endcode %}

{% code title="C:\winchecksec>" %}
```
cd build
```
{% endcode %}

* ทำการกำหนด Build System Generate

{% code title="C:\winchecksec\build>" %}
```
cmake -G "Visual Studio 15 2017 Win64" ..
```
{% endcode %}

```
CMake Warning (dev) in CMakeLists.txt:
  No project() command is present.  The top-level CMakeLists.txt file must
  contain a literal, direct call to the project() command.  Add a line of
  code such as

    project(ProjectName)

  near the top of the file, but after cmake_minimum_required().

  CMake is pretending there is a "project(Project)" command on the first
  line.
This warning is for project developers.  Use -Wno-dev to suppress it.

-- Selecting Windows SDK version 10.0.17763.0 to target Windows 10.0.18363.
-- The C compiler identification is MSVC 19.16.27034.0
-- The CXX compiler identification is MSVC 19.16.27034.0
-- Check for working C compiler: C:/Program Files (x86)/Microsoft Visual Studio/2017/Community/VC/Tools/MSVC/14.16.27023/bin/Hostx86/x64/cl.exe
-- Check for working C compiler: C:/Program Files (x86)/Microsoft Visual Studio/2017/Community/VC/Tools/MSVC/14.16.27023/bin/Hostx86/x64/cl.exe - works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: C:/Program Files (x86)/Microsoft Visual Studio/2017/Community/VC/Tools/MSVC/14.16.27023/bin/Hostx86/x64/cl.exe
-- Check for working CXX compiler: C:/Program Files (x86)/Microsoft Visual Studio/2017/Community/VC/Tools/MSVC/14.16.27023/bin/Hostx86/x64/cl.exe - works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- The following ICU libraries were not found:
--   uc (required)
-- Failed to find all ICU components (missing: ICU_INCLUDE_DIR ICU_LIBRARY _ICU_REQUIRED_LIBS_FOUND) (Required is at least version "55.0")
-- Build type: RelWithDebInfo
-- Build Shared: OFF
-- Build Command Line Tools: ON
-- Install prefix: /usr
-- Configuring done
-- Generating done
-- Build files have been written to: D:/Work/Git/winchecksec/build
```

* ทำการรัน Build Program

{% code title="C:\winchecksec\build>" %}
```
cmake --build . --config Release
```
{% endcode %}

```
Microsoft (R) Build Engine version 15.9.21+g9802d43bc3 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

  Checking Build System
  Building Custom Rule D:/Work/Git/winchecksec/pe-parse/pe-parser-library/CMakeLists.txt
  Microsoft (R) C/C++ Optimizing Compiler Version 19.16.27034 for x64
  Copyright (C) Microsoft Corporation.  All rights reserved.

  cl /c /I"D:\Work\Git\winchecksec\pe-parse\pe-parser-library\include" /Zi /W4 /WX /diagnostics:classic /O2 /Ob2 /D WIN32 /D _WINDOWS /D NDEBUG /D "CMAKE_INTDIR=\"Release\"" /D _MBCS /Gm- /EHsc /MD /GS /fp:precise /Zc:wchar_t /Zc:forSco
  pe /Zc:inline /GR /Fo"pe-parser-library.dir\Release\\" /Fd"pe-parser-library.dir\Release\pe-parser-library.pdb" /Gd /TP /analyze /errorReport:queue "D:\Work\Git\winchecksec\pe-parse\pe-parser-library\src\buffer.cpp" "D:\Work\Git\winch
  ecksec\pe-parse\pe-parser-library\src\parse.cpp" "D:\Work\Git\winchecksec\pe-parse\pe-parser-library\src\unicode_codecvt.cpp"

  buffer.cpp
  parse.cpp
  unicode_codecvt.cpp
  Compiling...
  Generating Code...
  pe-parser-library.vcxproj -> D:\Work\Git\winchecksec\build\pe-parse\pe-parser-library\Release\pe-parser-library.lib
  Building Custom Rule D:/Work/Git/winchecksec/pe-parse/dump-pe/CMakeLists.txt
  Microsoft (R) C/C++ Optimizing Compiler Version 19.16.27034 for x64
  Copyright (C) Microsoft Corporation.  All rights reserved.

  cl /c /I"D:\Work\Git\winchecksec\pe-parse\pe-parser-library\include" /Zi /W4 /WX /diagnostics:classic /O2 /Ob2 /D WIN32 /D _WINDOWS /D NDEBUG /D "CMAKE_INTDIR=\"Release\"" /D _MBCS /Gm- /EHsc /MD /GS /fp:precise /Zc:wchar_t /Zc:forSco
  pe /Zc:inline /GR /Fo"dump-pe.dir\Release\\" /Fd"dump-pe.dir\Release\vc141.pdb" /Gd /TP /analyze /errorReport:queue "D:\Work\Git\winchecksec\pe-parse\dump-pe\main.cpp"

  main.cpp
  dump-pe.vcxproj -> D:\Work\Git\winchecksec\build\pe-parse\dump-pe\Release\dump-pe.exe
  Building Custom Rule D:/Work/Git/winchecksec/CMakeLists.txt
  Checksec.cpp
d:\work\git\winchecksec\Checksec.h(28): warning C4275: non dll-interface class 'std::runtime_error' used as base for dll-interface class 'checksec::ChecksecError' [D:\Work\Git\winchecksec\build\winchecksec.vcxproj]
  C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Tools\MSVC\14.16.27023\include\stdexcept(157): note: see declaration of 'std::runtime_error'
  d:\work\git\winchecksec\Checksec.h(28): note: see declaration of 'checksec::ChecksecError'
d:\work\git\winchecksec\Checksec.h(57): warning C4251: 'checksec::Checksec::filepath_': class 'std::basic_string<char,std::char_traits,std::allocator>' needs to have dll-interface to be used by clients of class 'checksec::Ch
ecksec' [D:\Work\Git\winchecksec\build\winchecksec.vcxproj]
  C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\VC\Tools\MSVC\14.16.27023\include\xstring(4373): note: see declaration of 'std::basic_string<char,std::char_traits,std::allocator>'
     Creating library D:/Work/Git/winchecksec/build/Release/winchecksec.lib and object D:/Work/Git/winchecksec/build/Release/winchecksec.exp
  winchecksec.vcxproj -> D:\Work\Git\winchecksec\build\Release\winchecksec.dll
  Building Custom Rule D:/Work/Git/winchecksec/CMakeLists.txt
  Checksec.cpp
  main.cpp
  Generating Code...
  winchecksec-bin.vcxproj -> D:\Work\Git\winchecksec\build\Release\winchecksec.exe
  Building Custom Rule D:/Work/Git/winchecksec/CMakeLists.txt
```

* ทำการรันโปรแกรมด้วย Winchecksec

{% code title="" %}
```
.\Release\winchecksec.exe C:\Windows\notepad.exe
```
{% endcode %}

```
Dynamic Base    : true
ASLR            : true
High Entropy VA : true
Force Integrity : false
Isolation       : true
NX              : true
SEH             : true
CFG             : true
RFG             : false
SafeSEH         : false
GS              : true
Authenticode    : false
.NET            : false
```

**อ่านเพิ่มเติม** : [http://bit.ly/32Wujxv](http://bit.ly/32Wujxv)
