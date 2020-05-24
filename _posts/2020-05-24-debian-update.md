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

Solution
