---
layout: page
title: Notes
permalink: /notes/
---

1. Starting PRU: `echo "start" > state` won't work unless you are root user.<br>
Instead do `echo "start" | sudo tee -a state`.<br>
(This is in the directory(for pru0): `/sys/devices/platform/ocp/4a326004.pruss-soc-bus/4a300000.pruss/4a334000.pru/remoteproc/remoteproc1`)

2. Cloud 9:
The 'cloud9' directory is present in '/var/lib/cloud9/' when you log into the BeagleBoard.

3. Serial Connect to BeagleBoard
- Connect BBB via USB, open PuTTY.
- Select to the serial connect option.
- Check the newest serial line (COM port) by opening Device Manager (and checking the 'Ports(COM & LPT)') on Windows. (Might have to 'Show Hidden Devices') from the 'View' section in the toolbar
- Put that COMx value in PuTTY, then configure the Serial Line accordingly:
  - Speed(baud) = 15200
  - Data bits = 8
  - Stop bits = 1
  - Parity = None
  - Flow control = None
- Then click on 'Open'.
