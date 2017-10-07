# Intro to GPIO

## Blinking an LED

### Equipment Needed

* 270 or 330 Ohm Resistor
* LED
* Wires/Alligator Clips

### Installing the GPIO Zero Library
_gpiozero is a simple interface to GPIO [General Purpose Input Output] devices with Raspberry Pi_

`sudo apt-get install python3-gpiozero`

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

* `led = LED(17)` declares a variable for the LED and tells the Raspberry Pi which pin to listen to

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

   **NOTE** _Files cannot be run via python if they're not executable. Files whose permissions lines end with an `x` are executable, like: `-rwxr-xr-x`. Files without an `x` need to be modified so that python can run them._
   * Convert non-executable files to executable files:

   `sudo chmod +x filename.py`

#### 5. Run the script:
`ipython3 filename.py`
