---
layout: post
title: "Updating PRUSS-Bindings to the latest (2020) Debian Image and Kernel"
categories: GSoC
---
---------

The 'pruapi_1.0-2_armhf.deb' cannot be used for the `BeagleBoard.org Debian Buster IoT Image 2020-04-06`. This is because the kernel module `pruss_api.ko` was compiled for the `4.14.71-r80` kernel on `BeagleBoard.org Debian Image 2018-10-07` whereas the new Debian Image uses the version `4.19.94-ti-r42` kernel.

Use `$ cat /etc/issue` to find Debian version
Use `$ uname -r` to find your kernel version

The next step would be to 
1. complile `pruss_api.c` using the new kernel headers to get `pruss_api.ko`.
2. Make a new Debian package and release it as 
3. Document the process for Debian packaging and upload the required scripts so that anyone will be able to follow the steps

Just for reference; the error messages encountered while running 'pruapi_1.0-2_armhf.deb' on `BeagleBoard.org Debian Buster IoT Image 2020-04-06`: 
1. Upon installing the package, a new directory in `/lib/modules` is created with the incorrect kernel version name. It always needs to be `uname -r` for the device on which installation is being done.
2. Upon insmod: `insmod: ERROR: could not insert module pruss_api.ko: Invalid module format`

---

Process for building package from source: 
1. Download and install the kernel headers to build the kernel module. 
   ```
   debian@beaglebone:~$ sudo apt-get update
   debian@beaglebone:~$ apt-cache search linux-headers-$(uname -r)
   linux-headers-4.19.94-ti-r42 - Linux kernel headers for 4.19.94-ti-r42 on armhf
   debian@beaglebone:~$ sudo apt-get install linux-headers-4.19.94-ti-r42
   debian@beaglebone:~$ cd /usr/src/linux-headers-4.19.94-ti-r42
   ```
   Also `build` should now be visible in `/lib/modules/(uname -r)`
   
2. Use `checkinstall`. What checkinstall essentially does is that it runs `make install` and outputs a debian package with the binaries after asking a few questions. 

3. `checkinstall` usually came pre-installed but it is not available on the Buster Image :( probably because it is not maintained (last commit 2016) and that it has security issues.
   Check out [https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=878487](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=878487), and [https://serverfault.com/questions/974651/checkinstall-package-in-debian-buster](https://serverfault.com/questions/974651/checkinstall-package-in-debian-buster), checkinstall package for Debian Buster is now available thru buster-backports repo.
   
   Add backports to your sources.list:
   `deb http://deb.debian.org/debian buster-backports main`
   to your sources.list (or add a new file with the ".list" extension to /etc/apt/sources.list.d/) You can instead use https    when the apt-transport-https package is installed.

   Run apt-get update
   
4. `sudo apt-get -t buster-backports install checkinstall`: Checkinstall should now finally be installed.
   Important Resource: [https://backports.debian.org/Instructions/](https://backports.debian.org/Instructions/)
   
5. 
