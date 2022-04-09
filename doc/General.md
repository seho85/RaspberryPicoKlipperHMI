General
=======
Goal of this project was to make an HMI for controlling klipper.

Goals:
* Easy integration into Klipper
* Only one cable to the device that runs klipper (e.G. Raspberry PI).
* Having a hardware "Emergency Stop" Button.

Using:
* 4x20 Character LCD (HD44780)
* 8 Buttons that can be used in Klipper to perform any defined action.
* 7 LEDs that can also be individually controlled from Klipper.
* Rotary encoder with push button for controlling the menu.

KiCad Projects
--------------
Two KiCad Projects were included here:

* RPIPicoAsciHMI2
  * The Project for the Display that i use with klipper on my printer
* RPiPicoKlipperAsciiHMI
  * The project where i started from (runned on a breadboard)

**WARNING: 
The Pins used in the KiCAD projects are not the same!**

For details how the PCB are connected please refer to the KiCad Projects.