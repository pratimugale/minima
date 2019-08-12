---
layout: post
title: "Debian Packaging"
categories: GSoC
---

In this post, I'll explain how I went about doing the Debian Packaging of the project.
`dpkg` is already installed on the BeagleBone Black.<br>
`checkinstall` is NOT installed.<br>
`$ sudo apt-get update`<br>
`$ sudo apt-get install checkinstall`<br>
525kB of additional disk space was used.<br>

DEBIAN NEW MAINTAINER'S GUIDE:
1. debian@beaglebone:~/debian-packaging$ tar --exclude-vc -cvf pruapi-0.5.tar.gz PRUSS-Bindings/
2. THE ABOVE WON'T make a GZIP file even when it is named .gz
3. Instead do: debian@beaglebone:~/debian-packaging$ tar --exclude-vcs -czvf pruapi-0.5.tar.gz PRUSS-Bindings/
'z' is added in this. --exclude-vcs gets rid of all the version control files like .git and .gitignore.
4. debian@beaglebone:~/debian-packaging/PRUSS-Bindings$ cat >>~/.bashrc <<EOF
DEBEMAIL="pratim.ugale@gmail.com"
DEBFULLNAME="Pratim Ugale"
export DEBEMAIL DEBFULLNAME
EOF
5. . ~/.bashrc

7. dh_make -f ../pruapi-0.5.tar.gz


### References:
1. [https://wiki.debian.org/Packaging/Intro?action=show&redirect=IntroDebianPackaging](https://wiki.debian.org/Packaging/Intro?action=show&redirect=IntroDebianPackaging)
2. [https://wiki.debian.org/HowToPackageForDebian](https://wiki.debian.org/HowToPackageForDebian)
