
## Install Docker :
### 1. Go [here](https://docs.docker.com/get-docker/)
### 2. In my case, since i had Windows 11 i install using the `Windows Terminal` in admin mode. 
``` powershell
PS C:\Users\joaoc> wsl --install
Installing: Virtual Machine Platform
Virtual Machine Platform has been installed.
Installing: Windows Subsystem for Linux
Windows Subsystem for Linux has been installed.
Downloading: WSL Kernel
Installing: WSL Kernel
WSL Kernel has been installed.
Downloading: GUI App Support
Installing: GUI App Support
GUI App Support has been installed.
Downloading: Ubuntu
The requested operation is successful. Changes will not be effective until the system is rebooted.
```
## After reboting a terminal will appear automatically that will ask to define a user account for "new OS" :

![image](https://user-images.githubusercontent.com/49458268/180616369-2ca57d0d-72c9-44a3-9ba9-826add09acb9.png)

## To check if we have virtualization enabled on BIOS we see on `Task Manager` : 

![image](https://user-images.githubusercontent.com/49458268/180617220-1501b6d8-bda1-4661-b3d5-7df1fe0eeef5.png)

## To check if the CPU supports SLAT we use a microsoft tool called [CoreInfo](https://docs.microsoft.com/en-us/sysinternals/downloads/coreinfo)

``` powershell
PS C:\MySoftware\Docker-related-software\Coreinfo> .\Coreinfo.exe -v

Coreinfo v3.52 - Dump information on system CPU and memory topology
Copyright (C) 2008-2021 Mark Russinovich
Sysinternals - www.sysinternals.com


Note: Coreinfo must be executed on a system without a hypervisor running for
accurate results.

AMD Ryzen 7 5800H with Radeon Graphics
AMD64 Family 25 Model 80 Stepping 0, AuthenticAMD
Microcode signature: 00000000
HYPERVISOR      *       Hypervisor is present
SVM             -       Supports AMD hardware-assisted virtualization
NP              -       Supports AMD nested page tables (SLAT)
```
## Check if Docker Engine is running : 
![image](https://user-images.githubusercontent.com/49458268/180646117-c8df7efb-21b2-48fa-a261-ad51a5ed17c3.png)
