# PX4 Autopilot

PX4 is an open-source BSD-3 Licensed autopilot system for unmanned aerial vehicles (UAVs) It provides both hardware and software components to control various types of drones, from small quadcopters to fixed-wing aircraft and even autonomous vehicles like rovers and boats.

# Serial port mapping

| UART    | Device     | Port   |
|---------|------------|--------|
| LPUART6 | /dev/ttyS0 | DEBUG  |
| LPUART2 | /dev/ttyS1 | GPS    |
| LPUART3 | /dev/ttyS2 | TELEM1 |
| LPUART4 | /dev/ttyS3 | AUX    |
| LPUART5 | /dev/ttyS2 | TELEM2 |
| LPUART7 | /dev/ttyS5 | ESC    |
| LPUART8 | /dev/ttyS6 | RC     |

# Flashing the PX4 Bootloader to MR-VMU-Tropic

If your board does not come pre-installed with a PX4-compatible bootloader, you’ll need to flash one manually.
You can download the official PX4 bootloader here [nxp_mr-tropic_bootloader.bin](https://github.com/PX4/PX4-Autopilot/raw/0b7860bfe57ad171ee596492787d05756041c5be/boards/nxp/mr-tropic/extras/nxp_mr-tropic_bootloader.bin).

To flash the PX4 bootloader using USB, you can follow the steps in the official guide https://docs.px4.io/main/en/advanced_config/bootloader_update_v6xrt.</br>
However, make the following adjustments:

- Replace all mentions of MIMXRT1170 with MIMXRT1064.
- Skip Step 4: Boot Memory Configuration, this step is not needed for this board.


Alternatively, you can connect a debugger like J-Link via SWD and flash the bootloader directly using tools like J-Link Commander or J-Flash.

# Building PX4 for MR-VMU-Tropic

First you need to setup your build environment. The PX4 user guide provides a [Developer Environment guide](https://docs.px4.io/main/en/dev_setup/dev_env.html). There you can select the corresponding guide for your platform, [Ubuntu](https://docs.px4.io/main/en/dev_setup/dev_env_linux_ubuntu.html), [Windows](https://docs.px4.io/main/en/dev_setup/dev_env_windows_wsl.html), [macOS](https://docs.px4.io/main/en/dev_setup/dev_env_mac.html).

After setting up your build environment enter the `PX4-Autopilot` folder and type the following command to build PX4
```
make nxp_mr-tropic
```

# Flashing PX4 Firmware with QGroundControl

> [!NOTE]  
> You need a [daily build](https://docs.qgroundcontrol.com/master/en/qgc-user-guide/releases/daily_builds.html) of QGroundControl to get autodetect work

1. Start QGroundControl on your computer.
2. Go to the Firmware tab:  
   Click the gear icon (Vehicle Setup) → Select Firmware from the sidebar.
3. Put your board in bootloader mode:  
   Disconnect all power sources (USB and battery), then connect the board via USB directly to your computer (not through a hub).
4. QGC will detect the board and show firmware options.
5. Choose PX4 Flight Stack and select the desired version (Stable is recommended),  
   or manually select a custom firmware file that you’ve compiled locally.
6. Click OK to begin flashing.  
QGC will download (or use your file), erase, and flash the firmware automatically.
7. Once done, the board will reboot and reconnect.

# QGroundControl

Once PX4 has been flashed on the MR-VMU-Tropic, Connect the MR-VMU-Tropic to your PC through USB and launch [QGroundControl](http://qgroundcontrol.com/) to configure your MR-VMU-Tropic.

For more information on how to configure PX4 checkout the [PX4 configuration guide](https://docs.px4.io/main/en/config/)

# PX4 MR-VMU-Tropic test

The first revision of the MR-VMU-Tropic has been tested with PX4 has been tested on a small quad in autonomous flight.

## PX4 Testing Flight Logs:
1. https://review.px4.io/plot_app?log=e7aa735b-a087-448f-ad0c-712ef94dfce5
