# johnnyws-linux-distro
The goal of this project is to create a collection of scripts to facilitate
building a lightweight Linux-based OS from source, targeted at desktop
computing on x86_64 systems. Currently, I am working on developing Jenkins build scripts for the needed
Linux utilities and running the scripts on my Jenkins server
[here](https://www.johnnyw.ca/jenkins/job/linux-apps). I am taking inspiration
from the excellent [LFS book](https://www.linuxfromscratch.org/lfs/), but am not
aiming for full LFS-compilance and have been taking liberties to better suit the
system to my particular needs. A list of these key differences from this project
and LFS will be included here as the project progresses.

## Packages included
Package | Version | Status
:---|:---|:---:
LLVM | 18.1.0-rc2 | [![Build Status](https://www.johnnyw.ca/jenkins/buildStatus/icon?job=linux-apps%2Fllvm-18.1)](https://www.johnnyw.ca/jenkins/job/linux-apps/job/llvm-18.1/)
Linux Kernel (headers) | 6.6.16 | [![Build Status](https://www.johnnyw.ca/jenkins/buildStatus/icon?job=linux-apps%2Flinux-kernel-headers-6.6)](https://www.johnnyw.ca/jenkins/job/linux-apps/job/linux-kernel-headers-6.6/)
glibc | 2.39 | Not in repo
