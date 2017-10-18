# Viewing Photos on RSP


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
3. Setup an application [Here]:https://www.dropbox.com/developers/apps
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
