Klipper Patches
===============
The LCD Module may need some tweaks in the klipper sourcecode to work properly.

You can find out easily if you need this patches.

When your display just show garbage, the you need this patch.


I created this patch and also created a pull request that this changes can be merged into the main klipper source.

Unfortunately integrating this changes is currently denied, because there are not at least 100 people that would benified from the changes.

**So please, if you encounter this problem add a comment to my [pull request](https://github.com/Klipper3d/klipper/pull/5318)**

You can patch your own sourcetree with the patch provided below or just take the whole [hd44780.py](https://raw.githubusercontent.com/seho85/klipper/master/klippy/extras/display/hd44780.py) file from my klipper fork, that integrates that changes.

What does the patch provide
---------------------------
If your display just shows garbage it's most likely cost by the strict timings that were used to controll the LCD per it's paralell interface.

The Patch gives you the opportunity to lower this strict timings.

Patch
-----
```
klippy/extras/display/hd44780.py

@@ -12,8 +12,6 @@

TextGlyphs = { 'right_arrow': b'\x7e' }

HD44780_DELAY = .000040

class HD44780:
    def __init__(self, config):
        self.printer = config.get_printer()
@@ -48,13 +46,17 @@ def __init__(self, config):
             0xc0),
            # Glyph framebuffer
            (self.glyph_framebuffer, bytearray(b'~'*64), 0x40) ]
        self.initialization_delay = config.getfloat("hd44780_init_delay",
            .100, .100, 1.0)
        self.display_pin_delay = config.getfloat("hd44780_pin_delay", .00004,
            .00004, 1.0)
    def build_config(self):
        self.mcu.add_config_cmd(
            "config_hd44780 oid=%d rs_pin=%s e_pin=%s"
            " d4_pin=%s d5_pin=%s d6_pin=%s d7_pin=%s delay_ticks=%d" % (
                self.oid, self.pins[0], self.pins[1],
                self.pins[2], self.pins[3], self.pins[4], self.pins[5],
                self.mcu.seconds_to_clock(HD44780_DELAY)))
                self.mcu.seconds_to_clock(self.display_pin_delay)))
        cmd_queue = self.mcu.alloc_command_queue()
        self.send_cmds_cmd = self.mcu.lookup_command(
            "hd44780_send_cmds oid=%c cmds=%*s", cq=cmd_queue)
@@ -98,7 +100,8 @@ def init(self):
        # Reset (set positive direction ; enable display and hide cursor)
        init.append([0x06, 0x0c])
        for i, cmds in enumerate(init):
            minclock = self.mcu.print_time_to_clock(print_time + i * .100)
            minclock = self.mcu.print_time_to_clock(
                print_time + i * self.initialization_delay)
            self.send_cmds_cmd.send([self.oid, cmds], minclock=minclock)
        self.flush()
    def write_text(self, x, y, data):
```

