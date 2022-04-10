>  **DISCLAIMER:**
>   This project project is made by an hobbyist.
>   Everything described here is without guarantee, so if you perform something described here, **YOU DO IT ON YOUR OWN RISK**
>
ASCII Display for Klipper
=========================

This project contains the ASCII Display that I use with Klipper.

It's controlled by a Rotary Encoder and few Buttons and controllable LEDs.

![HMI](doc/img/HMI.jpg)

The Display used is an 20x4 Display, the brightness of the backgroundlight LED can be controlled from klipper.

A Raspberry Pi Pico is used as MCU Module.

See [General](doc/General.md) for details.

KiCAD Projects
--------------
Two KiCAD projects can be found.

* _RPiPicoKlipperAsciiHMI_
  * Schematics I used on my breadboard during "proof of concept" phase.
* _RPiPicoAsciiHMI2_
  * [Schematics](../RaspberryPicoKlipperHMI/RPiPicoAsciiHMI2/Schematic.pdf) for the HMI that I use with klipper.


See [KiCAD Projects](doc/KiCAD_Projects.md)


PCBs
----
Basically the whole HMI consists of two PCBs.

* The [Button PCB](doc/BTN_LED_PCB.md)
    * Buttons (with integrated LEDs)
* The [Main PCB](doc/Main_PCB.md)
  * all other components.

FreeCAD Projects
----------------
In the _FreeCAD_ folder two FreeCAD Projects for the case and the backcover can be found.


Hardware used
-------------
See [Hardware](Hardware.md)

Klipper Configuration
---------------------
See [Klipper Config](KlipperConfig.md)

How to Flash Raspberry Pi Pico
------------------------------
See [Flashing](Flashing.md)