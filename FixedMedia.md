# Set up pi to play fixed media

(original source: https://oshlab.com/raspberry-pi-fireplace-video-looper/)

Install 'omxplayer'
> 'sudo apt-get install omxplayer'

Go into config file
> 'cd /boot/config.text'

Save and exit after making 2 changes:
1. Uncomment '#hdmi_force_hotplug=1'
2. Uncomment '#hdmi_group' and '#hdmi_mode' and make sure numbers are set at 1 and 16, respectively


# Downloading videos from YouTube

Install 'youtube downloader'
> 'sudo apt-get install youtube-dl'

Copy the URL of the YouTuvbe video you want to play from pi
> 'youtube-dl <PASTE URL HERE>'


#Changing downloaded video file name

Use the 'mv' command to change the name
> 'mv [OLD FILE NAME] [NEW FILE NAME]'
> Example: 'mv Nyan\ Cat\ \[original\]-QH2-TGUlwu4.mp4 nyan_cat.mp4'
> To avoid spaces, use the TAB key to write out the old file name.

To play the video:
> 'omxplayer [YOUR FILE NAME]'
> Example: 'omxplayer nyan_cat.mp4'


# Running Loop for Videos

Open `rc.local`
> nano /etc/rc.local

Scroll until you see `exit 0`, which has to be the last line on the file.

Loop All
> `loop_all.sh`, with bash in the background.
> Critical: Check `su -c "sh/path/to/file/loop_all.sh" pi &`

Save and exit.

Next, `sudo reboot now`

Make sure `loop_all.sh` has been made executable
> with  `chmod +x loop_all.sh`

Stop the looping process from launching on boot: Comment Out, starting with `#`, to revert to non-looping functionality.

Save > Exit > Reboot > Confirm

Point `rc.local` to `loop_one.sh` for a single video
> Result: `su -c "sh/path/to/file/loop_one.sh" pi &`


#To loop the video:
> 'omxplayer --loop [YOUR FILE NAME]'
> Example: 'omxplayer --loop nyan_cat.mp4

To create a black background for the video:
> 'omxplayer -b [YOUR FILE NAME]'

To hide on-screen dialogue messages:
> 'omxplayer --no-osd [YOUR FILE NAME]'

To force audio output via the HDMI cable:
> 'omxplayer -o hdmi [YOUR FILE NAME]'

To achieve all of the above functions:
>'omxplayer -b --loop --no-osd -o hdmi [YOUR FILE NAME]'
> Example:'omxplayer -b --loop --no-osd -o hdmi nyan_cat.mp4'


#looping one video forever
1. make a folder called videolooper: 'mkdir videolooper'
2. Enter the videolooper folder: 'cd videolooper'
3. make a video folder inside videolooper: 'mkdir video'
4. make a new file called loop_one.sh: 'touch loop_one.sh'
5. open up loop_one.sh in atom: 'atom loop_one.sh'
6. Copy and paste 'omxplayer -b --loop --no-osd -o hdmi /home/pi/nyan_cat.mp4' into your loop_one.sh file
7. Send loop_one.sh to your raspberry pi: 'scp loop_one.sh pi@<PI_IP_ADDRESS>:/home/pi/'
8. Make loop_one.sh executable: 'chmod: chmod +x loop_one.sh'
9. Run loop_one.sh: './loop_one.sh'
