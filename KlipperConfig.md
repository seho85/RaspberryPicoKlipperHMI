Klipper Configuration
=====================

Patch
-----
Some LCD character displays like mine doesn't work with actual version (v0.10.0-272), they were just utilized to fast on the paralell display interface.

I created a [pull request](https://github.com/Klipper3d/klipper/pull/5318) that delays (which were already defined - but hardcoded) can be configured in the configuration file.
But untils it's not accepted and merged into the codebase of klipper a single file needs to be patched.

Please see the [pull request](https://github.com/Klipper3d/klipper/pull/5318) which tweaks needed to be made. Or to find out if tweaks need to be made at all.


Configuration
-------------
Till the last two parameters in the configuration pretty much everything in configuration is default [klipper display configuration](https://www.klipper3d.org/Config_Reference.html#display-support)

The _hd44780_init_delay_ and _hd44780_pin_delay_ controll the delay for utilizing the paralell interface of the the display.

If your display works, you try to lower the value until not works anymore, to find the delay your actual display needs.

If you see just gibberish output on your display, you may need to increase this delays.

```
[mcu rp_pico]
serial: /dev/serial/by-id/usb-Klipper_rp2040_E6611C08CB077322-if00
baud: 250000

[output_pin pico_led]
pin: rp_pico:gpio25

[output_pin lcd_backlight]
pin: rp_pico:gpio15
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

#control button pins (pulled up)
up_pin: ^rp_pico:gpio7
down_pin: ^rp_pico:gpio8
back_pin:^rp_pico:gpio10

#Internal Pulled Up - Low Active
#Dangerous config - no wire break detection
kill_pin: ^!rp_pico:gpio6

# Rotary Encode Module
click_pin: ^rp_pico:gpio9
encoder_pins: rp_pico:gpio11,rp_pico:gpio12

#Attention: Needs Patch
hd44780_init_delay: .200
hd44780_pin_delay: .0004
```