---
layout: post
title: "Kernel OOPS"
categories: GSoC
---

### dmesg logs:
```
// When showing the oops message:

$ dmesg
[  209.638868] remoteproc remoteproc2: powering up 4a338000.pru
[  209.652589] remoteproc remoteproc2: Booting fw image am335x-pru1-fw, size 74736
[  209.655820] pruss 4a300000.pruss: configured system_events[63-0] = 0x00000000.000c0000
[  209.655841] pruss 4a300000.pruss: configured intr_channels = 0x0000000a host_intr = 0x0000000a
[  209.663057] remoteproc remoteproc2: registered virtio0 (type 7)
[  209.663078] remoteproc remoteproc2: remote processor 4a338000.pru is now up
[  209.778529] virtio_rpmsg_bus virtio0: creating channel rpmsg-pru addr 0x1f
[  209.784149] virtio_rpmsg_bus virtio0: rpmsg host is online
[  209.844744] Unable to handle kernel NULL pointer dereference at virtual address 000001dc
[  209.854295] rpmsg_pru virtio0.rpmsg-pru.-1.31: new rpmsg_pru device: /dev/rpmsg_pru31
[  209.861249] pgd = dc628000
[  209.863991] [000001dc] *pgd=00000000
[  209.879449] Internal error: Oops: 5 [#1] PREEMPT SMP ARM
[  209.884813] Modules linked in: rpmsg_pru virtio_rpmsg_bus rpmsg_core pruss_soc_bus evdev uio_pdrv_genirq uio 8021q garp mrp stp llc usb_f_mass_storage usb_f_acm u_serial usb_f_ecm usb_f_rndis u_ether libcomposite iptable_nat nf_conntrack_ipv4 nf_defrag_ipv4 nf_nat_ipv4 nf_nat nf_conntrack iptable_mangle iptable_filter spidev pru_rproc pruss pruss_intc ip_tables x_tables
[  209.917848] CPU: 0 PID: 2175 Comm: prussd.py Not tainted 4.14.71-ti-r80 #1
[  209.924753] Hardware name: Generic AM33XX (Flattened Device Tree)
[  209.930875] task: db14c000 task.stack: db162000
[  209.935446] PC is at rpmsg_pru_write+0x80/0x108 [rpmsg_pru]
[  209.941045] LR is at 0x35
[  209.943676] pc : [<bf1a32c8>]    lr : [<00000035>]    psr: 600f0013
[  209.949970] sp : db163f00  ip : 0000001c  fp : db163f1c
[  209.955217] r10: 00000004  r9 : b5403b38  r8 : 00000000
[  209.960464] r7 : db163f68  r6 : 00000051  r5 : daac9210  r4 : 00000004
[  209.967019] r3 : 00000000  r2 : 00000004  r1 : bf1a52c4  r0 : 00000000
[  209.973577] Flags: nZCv  IRQs on  FIQs on  Mode SVC_32  ISA ARM  Segment none
[  209.980743] Control: 10c5387d  Table: 9c628019  DAC: 00000051
[  209.986514] Process prussd.py (pid: 2175, stack limit = 0xdb162218)
[  209.992809] Stack: (0xdb163f00 to 0xdb164000)
[  209.997190] 3f00: bf1a3248 dc532e40 b5403b38 db163f68 db163f34 db163f20 c02f9258 bf1a3254
[  210.005408] 3f20: 00000004 dc532e40 db163f64 db163f38 c02f943c c02f923c c031b088 c031af50
[  210.013626] 3f40: c1504dc8 dc532e41 00000000 00000000 dc532e40 b5403b38 db163fa4 db163f68
[  210.021843] 3f60: c02f96a4 c02f9394 00000000 00000000 db163fa4 77533b88 c030e73c b53ff940
[  210.030060] 3f80: 0076f000 b6f0dce8 00000004 c01090e4 db162000 00000000 00000000 db163fa8
[  210.038277] 3fa0: c0108f00 c02f9654 b53ff940 0076f000 00000004 b5403b38 00000004 00000000
[  210.046493] 3fc0: b53ff940 0076f000 b6f0dce8 00000004 b5403b38 00000004 0076f000 b5e00e38
[  210.054710] 3fe0: 00000000 b53fe0c0 00000000 b6eaf3d0 000f0030 00000004 00000000 00000000
[  210.062985] [<bf1a32c8>] (rpmsg_pru_write [rpmsg_pru]) from [<c02f9258>] (__vfs_write+0x28/0x48)
[  210.071821] [<c02f9258>] (__vfs_write) from [<c02f943c>] (vfs_write+0xb4/0x1c0)
[  210.079168] [<c02f943c>] (vfs_write) from [<c02f96a4>] (SyS_write+0x5c/0xbc)
[  210.086264] [<c02f96a4>] (SyS_write) from [<c0108f00>] (ret_fast_syscall+0x0/0x54)
[  210.093875] Code: 1a000012 e5953000 e1a02004 e59f1080 (e59301dc) 
[  210.145550] ---[ end trace b62e60d2f08e12c2 ]---


// Second time onwards (No message shown):

[  210.145550] ---[ end trace b62e60d2f08e12c2 ]---
[  334.539471] pruss 4a300000.pruss: unconfigured system_events[63-0] = 0x00000000.000c0000
[  334.556965] pruss 4a300000.pruss: unconfigured host_intr = 0x0000000a
[  334.574058] remoteproc remoteproc2: stopped remote processor 4a338000.pru
[  334.613038] remoteproc remoteproc2: powering up 4a338000.pru
[  334.619696] remoteproc remoteproc2: Booting fw image am335x-pru1-fw, size 74736
[  334.631899] pruss 4a300000.pruss: configured system_events[63-0] = 0x00000000.000c0000
[  334.642556] pruss 4a300000.pruss: configured intr_channels = 0x0000000a host_intr = 0x0000000a
[  334.659783] virtio_rpmsg_bus virtio0: creating channel rpmsg-pru addr 0x1f
[  334.667721] rpmsg_pru virtio0.rpmsg-pru.-1.31: new rpmsg_pru device: /dev/rpmsg_pru31
[  334.679444] virtio_rpmsg_bus virtio0: rpmsg host is online
[  334.694795] remoteproc remoteproc2: registered virtio0 (type 7)
[  334.710589] remoteproc remoteproc2: remote processor 4a338000.pru is now up
[  339.863605] pruss 4a300000.pruss: unconfigured system_events[63-0] = 0x00000000.000c0000
[  339.881557] pruss 4a300000.pruss: unconfigured host_intr = 0x0000000a
[  339.898184] remoteproc remoteproc2: stopped remote processor 4a338000.pru
[  339.914426] remoteproc remoteproc1: powering up 4a334000.pru
[  339.925698] remoteproc remoteproc1: Booting fw image am335x-pru0-fw, size 35856
[  339.933318] remoteproc remoteproc1: remote processor 4a334000.pru is now up
```

### kernel oops message:
Getting the message after writing 15 values.

```
$ ./test.o 
Wave 1 Sample 0
Wave 2 Sample 0
Wave 3 Sample 0
Wave 4 Sample 0
Wave 5 Sample 0
Wave 6 Sample 0
Wave 7 Sample 0
Wave 8 Sample 0
Wave 1 Sample 1
Wave 2 Sample 1
Wave 3 Sample 1
Wave 4 Sample 1
Wave 5 Sample 1
Wave 6 Sample 1
Wave 7 Sample 1
Wave 8 Sample 1

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.457337] Internal error: Oops: 5 [#1] PREEMPT SMP ARM

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.564394] Process prussd.py (pid: 2233, stack limit = 0xdc5c0218)

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.570689] Stack: (0xdc5c1f00 to 0xdc5c2000)

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.575072] 1f00: bf1b3248 dc67d480 b5503b38 dc5c1f68 dc5c1f34 dc5c1f20 c02f9258 bf1b3254

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.583289] 1f20: 00000004 dc67d480 dc5c1f64 dc5c1f38 c02f943c c02f923c c031b088 c031af50

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.591506] 1f40: c1504dc8 dc67d481 00000000 00000000 dc67d480 b5503b38 dc5c1fa4 dc5c1f68

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.599723] 1f60: c02f96a4 c02f9394 00000000 00000000 dc5c1fa4 77533b88 c030e73c b54ff940

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.607940] 1f80: 00743000 b6facce8 00000004 c01090e4 dc5c0000 00000000 00000000 dc5c1fa8

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.616156] 1fa0: c0108f00 c02f9654 b54ff940 00743000 00000004 b5503b38 00000004 00000000

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.624374] 1fc0: b54ff940 00743000 b6facce8 00000004 b5503b38 00000004 00743000 b5f00e38

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.632591] 1fe0: 00000000 b54fe0c0 00000000 b6f4e3d0 000f0030 00000004 00000000 00000000

Message from syslogd@beaglebone at Jul 31 04:06:26 ...
 kernel:[  128.671755] Code: 1a000012 e5953000 e1a02004 e59f1080 (e59301dc) 


```

Log: 

1. The kernel oops message shows up only when the BB is first booted. After that I tried unprobing and probing the pru_rproc, virtio_rpmsg_bus drivers and the oops message didn't show up.
2. Wrote a program to initialize the PRU SRAM to 0 to check what values are being written to the PRU SRAM in the oops case.
`No Values` were written to the PRU SRAM when the oops message shows up. Since the rpmsg program does the work of writing to the PRU SRAM, I think that no values were written to the RPMsg channel itself.
3. The order of execution of these lines is changed in the above two dmesgs: <br>
`virtio_rpmsg_bus virtio0: rpmsg host is online`
`rpmsg_pru virtio0.rpmsg-pru.-1.31: new rpmsg_pru device: /dev/rpmsg_pru31`
4. import prussd.py into another python program and try hardcoding the message.
