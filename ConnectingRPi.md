Connecting a Raspberry Pi
============

### FTDI BREAKOUT
1. Install FTDI Driver from [here](http://www.ftdichip.com/Drivers/VCP/MacOSX/FTDIUSBSerialDriver_v2_3.dmg).
2. Connect the PiWedge to Raspberry Pi and FTDI Basic Breakout to its spot on the wedge: with the microchip facing up, plug the breakout into the header pins on the corner of the PiWedge.
>**NOTE** Only use FTDI device of 3.3V or use 5V to 3.3V Logic Level Converter.

3. Plug the Raspberry Pi power adapter into its port and connect the other end to an outlet.

Reference images:

![alt text](https://github.com/Akashdman/chillin/blob/master/ftdi-plugged.jpg "FTDI to Piwedge")

![alt text](https://github.com/Akashdman/chillin/blob/bf46ea57e36723021ec5ddc2282c1646cf1d2322/wedge-n-pi.jpeg "Pi Wedge to Raspberry pi")

***

### CONNECTING PI VIA TERMINAL

#### Connecting via `screen`

1. Open a new terminal window and type the following command to connect to your Pi's console:
>Command line : `screen /dev/tty.usbserial` + `TAB` _to auto complete_

2. Add the BAUD rate : `115200` and press `ENTER`.
>Command line : `screen /dev/tty.usbserial-AH02LSSH 115200`

3. Press `enter` to bring up the login screen.
> **NOTE**  Once a connection is made you should notice that your terminal label will update to screen as opposed to bash.

4. Enter your login credentials.


#### Disconnecting from `screen`

1. Type `exit` and then hit `enter` to return to the login prompt.
2. Open a new terminal tab. `command+T`.
3. Enter `screen -ls` in the terminal and copy the Session number before `.tty001` for use in the next step.
4. Issue the following command in the terminal: `screen -X -S [session number] quit`

***

### TERMINAL

#### Setting up Wifi

1. Connect to Raspberry Pi via screen (see ‘Connecting via screen’ in the previous section).

2. Navigate to the file where you can save your wifi credentials:
>`cd /etc/wpa_supplicant/`

3. Open a Nano text file to edit your wifi credentials:
>‘sudo nano wpa_supplicant.conf’

4. You should see something like this:
>ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev update_config=1
<br><br>network={
<br><br>ssid="WIFINETWORKNAME"
<br><br>psk="WIFINETWORKPASSWORD"
<br><br>}

5. Replace ‘ssid’ and ‘psk’ with the credentials of your wifi network or add additional wireless network credentials below using the same format.
> **NOTE** The RPi will use the wireless networks in the order they're listed in the Nano file.

### Troubleshooting

#### Unsure if you're connected to the internet?

1. Connect to Raspberry Pi and open the wifi configuration file:
> Open the Folder: `cd /etc/wpa_supplicant/`
<br> Open the Text File: `sudo nano wpa_supplicant.conf`

2. Confirm that the ‘ssid’ and ‘psk’ in the file are correct.

3. Reboot your RPi.
> `sudo reboot now`

4. Log back into your RPi via `screen`.
5. Use `ping` to see if you are connected to the internet.
<br><br>**EXAMPLE** `ping wikipedia.org`
<br><br>**NOTE** If the internet is working, it should display a message like this:
>PING wikipedia.org (198.35.26.96): 56 data bytes
<br>64 bytes from 198.35.26.96: icmp_seq=0 ttl=52 time=16.948 ms
<br>64 bytes from 198.35.26.96: icmp_seq=1 ttl=52 time=17.714 ms
<br>64 bytes from 198.35.26.96: icmp_seq=2 ttl=52 time=16.952 ms

6. To end `ping`, press `CTRL`+ `C`.

#### Screen terminal is no responding

If somehow the screen terminal is not responding and you cannot connect your Raspberry pi. Try these different solutions mentioned below.

1. Check if any other session is still open by `screen -ls`. If yes kill it using `screen -X -S [session number] quit`

2. Check if the SD Card is inserted properly.

3. Format the SD card again and boot it again.

4. If screen acts wierd by getting stuck after intiating and does not show the login screen. 
* Try connecting it again by restarting your computer and raspberry pi.
* if still doesn't work, Use the an older mac/laptop of your teammate and connect it. 
* Find the IP address using `hostname -I`.
* Creat a new user on your raspberry pi. 
* Add the credentials of the nearest wifi network in `wpa_suppliment.conf` file. 
* Now, Use your own mac/system and connect your raspberry pi using wifi not by FDTI breakout. Make sure your system is connected to the same wifi network you added in raspberry config file. 
* now use `ssh pi@[hostname].local` hostname is the name of the user you added using your teammates laptop.
* if hostname is not find, check your wifi connection and check your credentials in 
* add your passowrd and have fun.

#### Alternate way to find IP address of pi

1. Connect to your pi using `ssh pi@[name].local` 
2. `sudo ifconfig`
3. Next to the `wlan0` entry you will see inet addr: 192.xxx.xxx.xxx or 10.xxx.xxx.xxx which is the IP address of the Raspberry Pi. 





