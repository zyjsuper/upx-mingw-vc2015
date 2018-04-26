1.download mysys2
http://repo.msys2.org/distrib/x86_64/msys2-x86_64-20161025.exe
2.Change Pacman install source:

first change mirrorlist.msys：as below

##
## MSYS2 repository mirrorlist
##

## Primary
## msys2.org
Server = http://mirrors.ustc.edu.cn/msys2/msys/$arch/
Server = http://repo.msys2.org/msys/$arch
Server = http://downloads.sourceforge.net/project/msys2/REPOS/MSYS2/$arch
Server = http://www2.futureware.at/~nickoe/msys2-mirror/msys/$arch/

---------------------------------------------------------------------------------------------------

first change  mirrorlist.mingw64：as below

##
## 64-bit Mingw-w64 repository mirrorlist
##

## Primary
## msys2.org
Server = http://mirrors.ustc.edu.cn/msys2/mingw/x86_64/
Server = http://repo.msys2.org/mingw/x86_64
Server = http://downloads.sourceforge.net/project/msys2/REPOS/MINGW/x86_64
Server = http://www2.futureware.at/~nickoe/msys2-mirror/x86_64/
Server = http://mirror.bit.edu.cn/msys2/REPOS/

---------------------------------------------------------------------------------------------------
first change  mirrorlist.mingw32：as below

##
## 32-bit Mingw-w64 repository mirrorlist
##

## Primary
## msys2.org
Server = http://mirrors.ustc.edu.cn/msys2/mingw/i686/
Server = http://repo.msys2.org/mingw/i686
Server = http://downloads.sourceforge.net/project/msys2/REPOS/MINGW/i686
Server = http://www2.futureware.at/~nickoe/msys2-mirror/i686/




3.update mysys2 and install compile tools.
a.
 pacman -Sy
 
b.open mingw64 shell terminal
 pacman -S mingw-w64-x86_64-gcc
 pacman -S make
 pacman -S mingw-w64-x86_64-cmake
 pacman -S mingw-w64-x86_64-pkg-config
 pacman -S zlib
 
 
4.compile ucl
git clone https://github.com/upx/upx/
cd upx
LZMA SDK from https://github.com/upx/upx-lzma-sdk
When using git run 'git submodule update --init --recursive'.
download from http://www.oberhumer.com/opensource/ucl/download/

after unzip it  
cd  ucl-1.03/B/
ls -l
-rw-r--r-- 1 zyjsuper 197121 2252 七月 20  2004 00README.TXT
-rw-r--r-- 1 zyjsuper 197121  188 七月 20  2004 clean.bat
-rw-r--r-- 1 zyjsuper 197121   59 七月 20  2004 done.bat
drwxr-xr-x 1 zyjsuper 197121    0 四月 25 21:16 dos16/
drwxr-xr-x 1 zyjsuper 197121    0 四月 25 21:16 dos32/
drwxr-xr-x 1 zyjsuper 197121    0 四月 25 21:16 generic/
drwxr-xr-x 1 zyjsuper 197121    0 四月 25 21:16 os2/
drwxr-xr-x 1 zyjsuper 197121    0 四月 25 21:16 os2_16/
-rw-r--r-- 1 zyjsuper 197121  185 七月 20  2004 prepare.bat
-rw-r--r-- 1 zyjsuper 197121  255 七月 20  2004 src.rsp
-rw-r--r-- 1 zyjsuper 197121  115 七月 20  2004 unset.bat
drwxr-xr-x 1 zyjsuper 197121    0 四月 25 21:16 win16/
drwxr-xr-x 1 zyjsuper 197121    0 四月 25 21:16 win32/
drwxr-xr-x 1 zyjsuper 197121    0 四月 25 21:16 win64/
---------------------------------------------------------------------------------------------------
open Visual Studio 2015 x64 terminal
run ./win64/vc_dll.bat  to generate ucl.dll
run ./win64/vc.bat to generate ucl.lib
download reimp from below url
https://sourceforge.net/projects/mingw/files/MinGW/Extension/mingw-utils
copy reimp.exe(all exe files) to C:\msys64\mingw64\bin
---------------------------------------------------------------------------------------------------
Open Msys2 MINGW64 Terminal
run 'reimp ucl.lib' to generate ucl.def
dlltool --dllname ucl.dll --def ucl.def --output-lib libucl.a 
copy libucl.a to C:\msys64\mingw64\x86_64-w64-mingw32\lib
---------------------------------------------------------------------------------------------------


5.compile UPX
Open Msys2 MINGW64 Terminal
go to UPX path
export UPX_UCLDIR=./ucl-1.03
make -C src