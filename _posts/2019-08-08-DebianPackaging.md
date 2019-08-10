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



### References:
1. [https://wiki.debian.org/Packaging/Intro?action=show&redirect=IntroDebianPackaging](https://wiki.debian.org/Packaging/Intro?action=show&redirect=IntroDebianPackaging)
2. [https://wiki.debian.org/HowToPackageForDebian](https://wiki.debian.org/HowToPackageForDebian)
