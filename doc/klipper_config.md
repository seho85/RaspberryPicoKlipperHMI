KlipperConfig for HMI
=====================

Here is complete configuration that contains everything that can be used in klipper.

Config Contents
---------------

This config contains the following elements:
* Display configuration for showing the Klipper Menu
  * Display configuration includes the defintions for the rotary encoder to controll the menu.
  * See [Klipper Patch](klipper_patches.md) for usage of the _hd44780_init_delay_ and _hd44780_pin_delay_ parameter.
* _output_pin_ definitions for the LEDs integrated in the buttons
* _gcode_btn_ definitions  for triggering user defined actions.
  * I use BTN1 (the one with allways on red LED) as Emergency Stop

Config
------
For the different sections you can find the documentation in the Klipper Configuration reference.
* [display](https://www.klipper3d.org/Config_Reference.html#display)
* [output_pin](https://www.klipper3d.org/Config_Reference.html#output_pin)
* [gcode_button](https://www.klipper3d.org/Config_Reference.html#gcode_button)
* [menu](https://www.klipper3d.org/Config_Reference.html#menu) for customizing the menu that is shown on pressing the button on the rotary encoder.

```
[mcu rp_pico]
serial: /dev/serial/by-id/usb-Klipper_rp2040_E660C0621359AD30-if00
baud: 250000
restart_method: command

[output_pin lcd_backlight]
pin: rp_pico:gpio28
pwm: true
cycle_time: 0.010
hardware_pwm: true
value: 1

[display]
lcd_type: hd44780
rs_pin: rp_pico:gpio0
e_pin: rp_pico:gpio1
d4_pin: rp_pico:gpio5
d5_pin: rp_pico:gpio4
d6_pin: rp_pico:gpio3
d7_pin: rp_pico:gpio2
hd44780_protocol_init: True
line_length: 20
menu_timeout: 30

# Rotary Encode Module
click_pin: ^rp_pico:gpio22
encoder_pins: rp_pico:gpio26,rp_pico:gpio27

#Attention: Patched Klipper is needed when the two following parameters were used.
hd44780_init_delay: .400
hd44780_pin_delay: .00055


#May be used for testing prints out 01234 on the second row in the second column on the display.
#display_group: static_text_grp

#[display_data static_text_grp static_text1]
#position: 1,1
#text: 01234


############
### LEDs ###

[output_pin btn2_led]
pin: rp_pico:gpio21

[output_pin btn3_led]
pin: rp_pico:gpio20

[output_pin btn4_led]
pin: rp_pico:gpio19

[output_pin btn5_led]
pin: rp_pico:gpio18

[output_pin btn6_led]
pin: rp_pico:gpio17

[output_pin btn7_led]
pin: rp_pico:gpio16

[output_pin btn8_led]
pin: rp_pico:gpio15

###############
### Buttons ###

#Emergency Stop BTN
[gcode_button btn1]
pin: ^!rp_pico:gpio6
press_gcode: M112

[gcode_button btn2]
pin: ^!rp_pico:gpio7
press_gcode: BTN2

[gcode_button btn3]
pin: ^!rp_pico:gpio8
press_gcode: BTN3

[gcode_button btn4]
pin: ^!rp_pico:gpio9
press_gcode: BTN4

[gcode_button btn5]
pin: ^!rp_pico:gpio10
press_gcode: BTN5

[gcode_button btn6]
pin: ^!rp_pico:gpio11
press_gcode: BTN6

[gcode_button btn7]
pin: ^!rp_pico:gpio12
press_gcode: BTN7

[gcode_button btn8]
pin: ^!rp_pico:gpio13
press_gcode: BTN8
```

Delay Parameters
----------------

hd44780_init_delay
------------------
The _hd44780_init_delay_ adds a delay on the intialization phase of the LCD Display, if you use a 4 line display and you see garbage on every 4 lines of the display you most likely **don't** need any tweaks for the settings.

If you 4 lines display just prints out stuff on the first and third line you may need to tweak this setting.

The default value used when setting is not provided is _0.100_ seconds

I you encounter problems that were described above add this too your _[display]_ sections, and increase the value till you got stuff on all 4 lines.


hd44780_pin_delay
-----------------
The _hd44780_pin_delay_ controlles the delay performed when a character is transmitted to the LCD Display.

When your display shows garbage on all 4 lines, you most likely need to tweak this setting.

The default value is 0.00004 sec if parameter is not used.

For finding out the delay for your display, add the configuration option and set it to _0.004_

When the display shows correct output try to lower the setting by factor ten, until you just got garbage printed out. Then increase the delay until you got reliable and good printings on your display.


