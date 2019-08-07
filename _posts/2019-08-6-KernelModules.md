---
layout: post
title: "Cross Compiling A Loadable Kernel Module for BeagleBone Black"
categories: GSoC
---

## Objective
To build an rpmsg driver that would expose dedicated sysfs files for the pruss-api.

## Steps Followed

### Build a Hello World Module first:
1. `sudo apt-get install git`
2. `git clone https://github.com/derekmolloy/exploringBB.git`
3. `sudo apt-get update` - IMPORTANT sometimes.
4. `apt-cache search linux-headers-$(uname -r)`<br>
linux-headers-4.14.71-ti-r80 - Linux kernel headers for 4.14.71-ti-r80 on armhf
5. ` sudo apt-get install linux-headers-4.14.71-ti-r80`<br>
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  linux-headers-4.14.71-ti-r80
0 upgraded, 1 newly installed, 0 to remove and 165 not upgraded.
Need to get 11.2 MB of archives.
After this operation, 77.7 MB of additional disk space will be used.
Get:1 http://repos.rcn-ee.com/debian stretch/main armhf linux-headers-4.14.71-ti-r80 armhf 1stretch [11.2 MB]
Fetched 11.2 MB in 39s (284 kB/s)                                                                                                             
Selecting previously unselected package linux-headers-4.14.71-ti-r80.
(Reading database ... 73929 files and directories currently installed.)
Preparing to unpack .../linux-headers-4.14.71-ti-r80_1stretch_armhf.deb ...
Unpacking linux-headers-4.14.71-ti-r80 (1stretch) ...
Setting up linux-headers-4.14.71-ti-r80 (1stretch) ...

6. `cd /usr/src/linux-headers-3.16.0-4-amd64/`<br>
   `ls`<br>
    arch  include  Makefile  Module.symvers  scripts
7. 
