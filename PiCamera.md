# PiCamera

## Reference

* [Getting Started with Pi Camera](https://www.raspberrypi.org/learning/getting-started-with-picamera/worksheet/)
* [PiCamera Docs](https://picamera.readthedocs.io/en/release-1.13/)
* [Andrea Fabrizi's Dropbox Uploader](https://github.com/andreafabrizi/Dropbox-Uploader)
* [GPAC (MP4Box Converter)](https://gpac.wp.imt.fr/mp4box/mp4box-documentation/)

## Equipment

* [PiCamera](https://www.adafruit.com/product/3099)
* [Pi Camera Adapter](https://www.adafruit.com/product/3157) (only needed if using with Pi Zero)

## Setup

1. Run the PiCamera setup script `sudo raspi-config`
2. Enable the camera in `Interfacing Options`
3. Plug the camera ribbon into the port labeled `CAMERA`.
 * Pull up on the socket cover.
 * Make sure the blue tape is facing the headphone jack.
 * Insert the tape until it clicks in and then push the socket cover back down.

 ![alt text](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2015/07/1436675540rpicamconnector.jpg)
4. Install the Python3 library for PiCamera `sudo apt-get install python3-camera`

## Take a Single Photo
Use the [Python3 code here](https://github.com/mediadesignpractices/fieldc_cheatsheets/blob/master/scripts/simple_photo.py) to take a single photo. How it works:

* To label each file with a unique filename, the script imports the `datetime` module and uses `datetime.now().strftime('%Y-%m-%d-%H-%m-%s')` to construct a filename comprised of the date and time down to the second.
* `camera.start_preview()` followed by a `sleep` statement allows the camera to calibrate and focus.
* `camera.capture()` stores, saves and names the photo file.
* `camera.stop_preview()` and `camera.close()` cleanup the setup required to take the photo.

## Viewing Photos on RSP

`camera.start_preview()`
Shows camera feed on connected display.

### By SCP
Steps to `scp` the images to your computer

1. `cd` to image location
2. On your _computer_ run `ifconfig` for IP address
3. On _pi_ use `scp` to send the file to computer. With `scp filename.jpg macbookUsername@macbookIPAddress:Path/To/Home`
> scp fieldcore.jpg Rathore@10.4.25.53:rathore/Desktop

4. Enter login password when asked, press `enter` to begin
5. Check the image in Preview


### Dropbox Uploader
Based on Andrea Fabrizi's dropbox uploader

1. On Pi, run `git clone https://github.com/andreafabrizi/Dropbox-Uploader.git`

2. On Computer, go to Dropbox. Login in your account.
3. Setup an application [Here](https://www.dropbox.com/developers/apps)
4. Click on `Create App`
> Select Dropbox API and Full Dropbox. Give your app a name, and confirm by clicking on `Create the app`

5. Click on `Generate access token`
> Keep the codes with you!

6. Run `bash` script: `./dropbox_uploader.sh`
7. When asked for the access token, give the code acquired at 5 and type `y` to confirm.
8. Try uploading `README.md` file in the Dropbox-Uploader folder to confirm functionality.
> ./dropbox_uploader upload README.md /

9. If successful, you'll see `> Uploading "/home/cta/Dropbox-Uploader/README.md" to "/README.md"... DONE`

10. On Computer, go to dropbox to check the transfer.

To upload photos, use
> ./dropbox_uploader.sh upload fileorfoldertoupload /

Keep in mind,
- You have to be in `Dropbox-Uploader` directory
- `/` that trialing slash is important!
- Works for single file, and directories.

## Simple Video

`camera.start_preview()`

gives the camera time to focus

`camera.start_recording()`

record video start command

`camera.stop_recording()`

record video stop command

`sleep()`

controls how long the video is

## Converting Video

> Note: Picamera saves video as Raw H264 Video Data. To view it on any display, convert it to MP4 using MP4Box converter.

_Follow the following steps to install:_

1. Download and install gpac on Pi: `sudo apt-get install -y gpac`
2. `cd` to the directory where your video lives and use MP4Box to convert your video to .mp4: `MP4Box -fps 30 -add myvid.h264 myvid.mp4`
3. Delete the original: 'rm mywid.h264'
4. Transfer the file to your Mac using scp :`scp myvid.mp4 [username]@IPaddressofmac /path/to`
5. Navigate to your `/path/to` and double click the .mp4 to watch.


# Deploying with the Pi Camera
The below script uses a (1) GPIO/toggle button function, and (2) LED light (sanity check) that becomes important for deployment.

To run this on boot, `cd` into `/etc/rc.local` and change path name to `su -c "python3 /path/to/[YOUR FILE NAME].py" pi &`

```python3
from gpiozero import Button
from gpiozero import LED
from picamera import PiCamera
from datetime import datetime
from time import sleep

# setup led and button
button = Button(2)
led = LED(17)

# recording flag
is_recording = 0

try:

    while True:
        if (button.value == True) and (is_recording == 0):

            camera = PiCamera()
            sleep(2)
            camera.start_preview()
            print("CALIBRATING...")
            print("READY TO RECORD!")
            print()
            print("RECORDING")
            x = datetime.now().strftime('%Y-%m-%d-%H-%m-%s')
            path = ''.join(['/home/pi/', x, '.h264'])
            camera.start_recording(path)
            is_recording = 1
            led.on()

        elif (button.value == False) and (is_recording == 1):
            print("DONE RECORDING!")
            camera.stop_recording()
            camera.stop_preview()
            led.off()
            camera.close()
            is_recording = 0


except KeyboardInterrupt:
    print("INTERRUPTED!")
    button.close()
    camera.close()
    led.close()
  ```
