# Intro to GPIO

## Blinking an LED

### Equipment Needed

* 270 or 330 Ohm Resistor
* LED
* Wires/Alligator Clips

### Installing the GPIO Zero Library
_gpiozero is a simple interface to GPIO [General Purpose Input Output] devices with Raspberry Pi_

`sudo apt-get install python3-gpiozero`

### Pin Numbering

![alt
text](https://github.com/Akashdman/chillin/blob/master/Pin%20layout.png)

### Turning on an LED

* Connect positive node of LED to `3V3` with a resister in between
* Connect negative node of LED to `GND`

### Understanding Blink Scripts

**What does a blink script look like?** In simplest terms, the basic structure of scripts used to blink an LED usually looks something like this: an infinite loop that can be interrupted by a keyboard command.

```python
try:
    while True:
        print("do stuff!")
except KeyboardInterrupt:
        print('interrupted!')
        print("Goodbye!")
```

Here is a more complex example that will blink an LED on for one second and off for one second *forever* until stopped by the keyboard interrupt command:

```python
from gpiozero import LED
from time import sleep

led = LED(17)

try:
    while True:
        print
        led.on()
        sleep(1)
        led.off()
        sleep(1)
except KeyboardInterrupt:
        print('interrupted!')
        led.close()
        print("Goodbye!")
```

To break down the anatomy of the above script...

* `from [LIBRARY] import [OBJECT]` imports the objects needed from a library to execute a given script

* `led = LED(17)` declares a variable for the LED and tells the Raspberry Pi which pin to listen to.

> Note: Pin can be changed according to use. Just make sure to connect the anode leg (Longer one) of LED to the same pin declared in the script.

* `try` clauses are used to anticipate errors and provide ways for the program to handle them. In effect, they instruct the computer to execute code, while offering procedures for what to do when errors occur in an `except` statement.

* `while True:` establishes an infinite loop in which a certain series of commands will be executed

* `led.on()` turns on the LED

* `led.off()` turns off the LED

* `sleep` refers to the length of time (in seconds) that an LED remains in a given state (on or off)

* `print("TEXT")` prints text in your terminal as the program runs

* `led.close()` frees up the designated pin (17)

### Blinking an LED with Raspberry Pi

#### 1. Connect the LED to the Raspberry Pi

* Connect positive node of LED to `GPIO Pin 17` with a resister in between
* Connect negative node of LED to `GND`

![alt text](http://fieldc.caseyanderson.com/assets/led-gpio17-hookup.png "Hookup GPIO Pin")

#### 2. Log into the Raspberry Pi wirelessly

   `ssh [USERNAME]@[HOSTNAME].local`

#### 3. Download blink scripts from GitHub repository

   * Under the repository name on GitHub, click `clone` or `download`
   * In the "Clone with HTTPs section," `copy` the URL for the repository
   * In your `TERMINAL` window, type
   `git clone [REPOSITORY URL]`

#### 4. Make sure the script is executable:

   * Navigate to the directory where you stored the cloned GitHub repository
   `cd [DIRECTORY NAME]`

   * Check to see which files in the directory are executable:
   `ls -la`

   >**NOTE** _Files cannot be run via python if they're not executable. Files whose permissions lines end with an `x` are executable, like: `-rwxr-xr-x`. Files without an `x` need to be modified so that python can run them._
   * Convert non-executable files to executable files:

   `sudo chmod +x filename.py`

#### 5. Run the script:
`ipython3 filename.py`

>use `ctrl-c` to interrupt

---

## Different Uses of Button

### Equipment Needed

* 270 or 330 Ohm Resistor
* LED
* Wires
* Button (momentary or toggle)

### Connection

Button does not have a Polarity. Connect one of the node to designated pin and another one to GND.


![alt text](http://fieldc.caseyanderson.com/assets/button.png)

### Use of button

#### 1. To perform a specified action using `ON/OFF` status of the button.

Example: Printing one of two messages to the terminal.

```python
from gpiozero import Button

button = Button(4)

try:
    while True:
        if button.is_pressed:
            print("Button is pressed")
        else:
            print("Button is not pressed")
except KeyboardInterrupt:
    print("interrupted!")
    button.close()
```

**Break down of the above script:**

* `from [gpiozero] import [button]` :
Imports `Button` object from the library `gpiozero`  

* `button = Button(4)`: This designates the `pin(4)` for the connection of Button. Connect any node of button to `gp4` pin on the PiWedge or Raspberry pi and the other one to `GND`.

* `if [button.is_pressed]`:
button.is_pressed is a predefined attribute in the 'Button' object imported from 'gpiozero' library. `if` creates a condition which checks the `ON/OFF` status of the button and responds in Boolean `True/False`.

* `else`: When the condition set by `if` is `False`, complier skips the statement of `if` and goes to the set of instruction provided after `else`.

* `KeyboardInterrupt`: A predefined function of python which creates a response when `ctrl-c` is pressed by the user during the execution of the command on the terminal shell.

* `button.close()`: Frees up the button from the designated pin.

#### 2. To turn ON/OFF an LED

Example 1
```python
from gpiozero import Button
from gpiozero import LED

button = Button(4)
led = LED(17)

try:
    while True:

        led.source = button.values

except KeyboardInterrupt:
    print("interrupted!")
    button.close()
    led.close()
```

OR

Example 2

```Python
from gpiozero import LED, Button
from signal import pause

led = LED(17)
button = Button(2)

button.when_pressed = led.on
button.when_released = led.off

pause()
```

**Break down of important line of in the both of the above script:**

* `from gpiozero import Button && import LED`:
imports Button and LED from gpiozero library

* `button = Button(4) | led = LED(17)`: designates the pins for button and LED.

* `led.source = button.values`: TBD

* `button.when_pressed = led.on`: turns on the LED when the button is kept at ON status.

* `button.when_released = led.off`: turns off the LED when button is kept at OFF status




> Link to Gpiozero Library functions : http://gpiozero.readthedocs.io/en/stable/index.html

---

## Troubleshooting
