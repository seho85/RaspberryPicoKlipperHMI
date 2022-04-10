How to flash Klipper to Raspberry Pi Pico
=========================================

Build klipper for Raspberry Pi Pico
-----------------------------------
1) Go to klipper directory
2) call _make menuconfig_
3) select
    * Micro-controller Architecture
        * Raspberry PI RP2040
    * Communication Interface
        * USB
4) save configuration
5) build firmware
    * call _make_
6) file needed for flashing can be found in
    * klipper/out/klipper.uf2


Flash Raspberry Pi Pico
-----------------------
1) Press the _BOOTSEL_ button on the Raspberry Pi Pico, 
2)  connected the USB cable.
    * The RPi Pico will be detected as USB flash device
3) Mount flash device
4) Copy _klipper.uf2_ to RPi Pico Flash Drive.
    * RPi Pico should now automatically perform a reboot and execute downloaded klipper firmware.
5) From now on the RPi Pico Module will be detected as an serial interface. Which can be configured in the klipper configuration.


During my development is created a small script which is placed in the klipper folder to automate the process of mounting, copying and unmounting.

Before executing it be sure that the RPi Pico is available at _/dev/sda1_

```
mkdir -p /tmp/rpi
sudo mount /dev/sda1 /tmp/rpi/
sudo cp out/klipper.uf2 /tmp/rpi/
sudo umount /tmp/rpi
```