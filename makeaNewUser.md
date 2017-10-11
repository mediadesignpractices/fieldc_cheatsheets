Make a new user
===============
Steps of commands

`1. sudo useradd -m -G pi,sudo,gpio,audio,video [NEWNAME]` Following command in the terminal

`2. sudo passwd [NEWNAME]` Change the password

`3. sudo reboot now` Restart your raspberry pi

### Change Hostname

`sudo nano /etc/hosts` initiates change process

`127.0.0.1 [Your New Hostname]` Change to desired hostname, and nothing else.

``[ctrl-x]``Save changes, and exit the file .

`sudo nano /etc/hostname` Issue command in terminal to initiate reboot
> sudo nano /etc/deploy


`sudo reboot now` to finish the process

Login again to confirm your change
