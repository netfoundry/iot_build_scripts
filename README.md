# iot_build_scripts
NetFoundry Scripts to build ZitiEdgeTunnel on IOT Devices

## Overview

The repository contains scripts to build/compile the ZET([ZitiEdgeTunnel](https://github.com/openziti/ziti-tunnel-sdk-c)) on several different IOT Devices.


## build_teltonika.bash 

This script builds the ziti-edge-tunnel for teltonika devices.

- you need to download and compile teltonika SDK first.
- modify the build script to have the right directory for the working directory and sdk directory
- run the build_teltonika.bash as root

### teltonika SDK compile

- [teltonika SDK](https://wiki.teltonika-networks.com/view/Software_Development_Kit) can be downloaded here, the build script was tested with **RUT9_R_00.07.05** SDK. 
- Use Ubuntu 20.04 OS (or 22.04 OS), don't use 18.04 as suggested in the instructions.
- Create a working direcotry, this will be our **ZT_WORKDIR** definition.
- Download and extract the SDK.
- Follow [teltonika compile instruction](https://wiki.teltonika-networks.com/view/RUTOS_Software_Development_Kit_instructions) to "**Compiling a standard firmware**".
- At the end of the successful compile, your directory should look like this:
```
$ pwd
/home/ubuntu/rutos-ath79-rut9-gpl
$ ls -l
total 98304
-rw-r--r--  1 root  root  100644952 Nov  1 03:23 RUT9_R_GPL_00.07.02.7.tar.gz
drwxr-xr-x 17 ziggy ziggy      4096 Nov  2 15:24 rutos-ath79-rut9-gpl
```

### build ziti-edge-tunnel

Put **build_teltonika.bash** anywhere on that build machine. Modify the definition of the following:
- ZT_WORKDIR="/home/ziggy/rutos-ath79-rut9-gpl"
- SDK_DIRNAME="rutos-ath79-rut9-gpl"

Make sure **build_teltonika.bash** is executable, then run the script:
```
sudo ./build_teltonika.bash
```

The compiled ziti edge tunnel binary (ziti-edge-tunnel) is under: ziti-tunnel-sdk-c-<version>/build/programs/ziti-edge-tunnel/

for example:
```
$ pwd
/home/ubuntu/rutos-ath79-rut9-gpl
$ ls -l
total 98304
-rw-r--r--  1 root  root  100644952 Nov  1 03:23 RUT9_R_GPL_00.07.02.7.tar.gz
drwxr-xr-x 17 ziggy ziggy      4096 Nov  2 15:24 rutos-ath79-rut9-gpl
-rw-r--r--  1 root  root        789 Nov  2 16:44 toolchain.cmake
drwxr-xr-x 15 root  root       4096 Nov  2 15:36 vcpkg
drwxr-xr-x 15 root  root       4096 Nov  2 15:36 ziti-tunnel-sdk-c-0.22.12
$ ls -l ziti-tunnel-sdk-c-0.22.12/build/programs/ziti-edge-tunnel/
total 4452
drwxr-xr-x 4 root root    4096 Nov  2 16:44 CMakeFiles
-rw-r--r-- 1 root root    2901 Nov  2 15:39 cmake_install.cmake
-rw-r--r-- 1 root root   19002 Nov  2 15:39 Makefile
-rwxr-xr-x 1 root root 4527012 Nov  2 16:44 ziti-edge-tunnel
```