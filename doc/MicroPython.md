MicroPython Testscripts
=======================
The Raspberry Pico Module can be programmed in MicroPython, which makes it handy for testing different components of the HMI.

Describing the whole process of setting up everything is beyond the scope of this description.

Here are a few links to get started with MicroPython on the PI Pico.

* https://www.raspberrypi.com/documentation/microcontrollers/micropython.html
* https://dev.to/blues/your-first-steps-with-raspberry-pi-pico-and-visual-studio-code-4jbd
* https://marketplace.visualstudio.com/items?itemName=ChrisWood.pico-go

This links should point you in the right direction to get the following testing scripts running. Which I heavily recommend for testing you soldering after checking the connections with an multimeter.

Also I know the scripts weren't very pretty, but the were hacked quick and dirty during the soldering session.


Buttons Test
------------
If this script is running on the Pi Pico, it creates an output when a button is pressed.

It can be used testing the connection of all the buttons.

Don't wonder if the message is printed more then once on a button press, this because the buttons are not debounced.

```
from machine import Pin
import machine
import time

btn1 = machine.Pin(6, Pin.IN, Pin.PULL_UP)
btn2 = machine.Pin(7, Pin.IN, Pin.PULL_UP)
btn3 = machine.Pin(8, Pin.IN, Pin.PULL_UP)
btn4 = machine.Pin(9, Pin.IN, Pin.PULL_UP)
btn5 = machine.Pin(10, Pin.IN, Pin.PULL_UP)
btn6 = machine.Pin(11, Pin.IN, Pin.PULL_UP)
btn7 = machine.Pin(12, Pin.IN, Pin.PULL_UP)
btn8 = machine.Pin(13, Pin.IN, Pin.PULL_UP)

def button_handler(pin):
    print("Button " + str(pin))
    time.sleep_ms(100)

btn1.irq(trigger=Pin.IRQ_FALLING, handler=button_handler)
btn2.irq(trigger=Pin.IRQ_FALLING, handler=button_handler)
btn3.irq(trigger=Pin.IRQ_FALLING, handler=button_handler)
btn4.irq(trigger=Pin.IRQ_FALLING, handler=button_handler)
btn5.irq(trigger=Pin.IRQ_FALLING, handler=button_handler)
btn6.irq(trigger=Pin.IRQ_FALLING, handler=button_handler)
btn7.irq(trigger=Pin.IRQ_FALLING, handler=button_handler)
btn8.irq(trigger=Pin.IRQ_FALLING, handler=button_handler)
```


LED Test
--------
This script toggles trough all the controllable LEDs integrated in buttons.

```
from machine import Pin
import machine
import time

led2 = machine.Pin(21, Pin.OUT)
led3 = machine.Pin(20,  Pin.OUT)
led4 = machine.Pin(19,  Pin.OUT)
led5 = machine.Pin(18,  Pin.OUT)
led6 = machine.Pin(17,  Pin.OUT)
led7 = machine.Pin(16,  Pin.OUT)
led8 = machine.Pin(15,  Pin.OUT)


leds = [ led2, led3, led3, led4, led5, led6, led7, led8]


for led in leds:
    led.high()
    time.sleep(1)
    led.low()
```


LCD Test
--------
To verifiy if the LCD is connected properly this script can be used.

It initializes the display and shows _000_ on the Display.

```
from machine import Pin
import time

bg = Pin(28, Pin.OUT, Pin.PULL_DOWN)

rs = Pin(0, Pin.OUT, Pin.PULL_DOWN)
e = Pin(1, Pin.OUT, Pin.PULL_DOWN)

d7 = Pin(2, Pin.OUT, Pin.PULL_DOWN)
d6 = Pin(3, Pin.OUT, Pin.PULL_DOWN)
d5 = Pin(4, Pin.OUT, Pin.PULL_DOWN)
d4 = Pin(5, Pin.OUT, Pin.PULL_DOWN)

def pulse():
    e.low()
    time.sleep_us(100);
    e.high()

def all_data_low():
    d7.low()
    d6.low()
    d5.low()
    d4.low()

#initial state
bg.high()

e.high()
rs.low()

all_data_low()

print("Waiting 10 seconds...\n");
#time.sleep(10)

time.sleep_ms(500)

d4.high()
d5.high()
pulse()

time.sleep_ms(10)
pulse()

time.sleep_ms(1)
d4.low()
pulse()

# display setup
d7.low()
d6.low()
d5.high()
d4.low()
pulse()
time.sleep_ms(1)

d7.high()
d6.low()
pulse()

time.sleep_ms(1)

#display off
d7.low()
d6.low()
d5.low()
d4.low()
pulse()

d7.high()
pulse()


# display on
all_data_low()
pulse()
time.sleep_us(100)

d7.high()
d6.high()
pulse()
time.sleep_us(100)


#print zero
rs.high()
all_data_low()
d4.high()
d5.high()
pulse()
time.sleep_us(100)
all_data_low()
pulse()
time.sleep_us(100)


all_data_low()
d4.high()
d5.high()
pulse()
time.sleep_us(100)
all_data_low()
pulse()
time.sleep_us(100)

all_data_low()
d4.high()
d5.high()
pulse()
time.sleep_us(100)
all_data_low()
pulse()
time.sleep_us(100)
```