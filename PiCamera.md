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
