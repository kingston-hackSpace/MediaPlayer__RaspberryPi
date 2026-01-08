# MediaPlayer__RaspberryPi
Run a video on start-up on a Raspberry pi. Use a HDMI screen (high resolution) / LCD TFT Display (low resolution).

----
## Set up your Raspberry Pi from scratch

If you have a brand new Raspberry Pi, you will need to start installing the Operating System (OS). 

If your Rpi already has its OS installed, *please skip this step.* 

[Tutorial: RPi set-up from scratch](https://github.com/kingston-hackSpace/RaspberryPi/blob/main/How_To_SetUp_Your_RPi_From_Scratch.md)

----
## A SCREEN FOR THE RPI

There are different screen options for your Rpi.

Read more [here](https://github.com/kingston-hackSpace/Display__RaspberryPi/tree/main)

----
# TUTORIAL

Run a video on start-up on a Raspberry pi using a screen with HDMI ports (for high resolution) or a LCD TFT Display (low resolution).

----
## Video formats

Compatible video formats: .mp4 / .mov / .mkv

Avoid: 4K videos, 60 fps videos, MPEG-2

Recommended (via HDMI):

  - .mp4

  - Video codec: H.264 (AVC)

  - Audio codec: AAC

  - Resolution: up to 1920×1080

  - Frame rate: 24–30 fps

----
## INSTALL VLC software

*Note: If VLC is already installed, you can skip this step*

- Turn on your Rpi

- Your Rpi must be connected to Ethernet or WIFI (Eduroam might not work).

- On the Desktop, create a folder called *videos*

- Using a USB stick, copy your videos into this folder. Keep a short name for your videos.

- Open the terminal and install VLC software by typing:

  ```
  sudo apt update
  sudo apt install vlc -y
  ```

----
## TEST your video on the RPi

- Turn on your RPi

- At Desktop, create a folder called *videos*

- Copy your video inside this folder

- Rename your video as *myvideo.mp4 / myvideo.mov* (depending on your video format)

- Open the terminal
  
- Check that the video file exists:

```
ls /home/hackspace/Desktop/videos
```

- Test the video using VLC:

```
vlc /home/hackspace/Desktop/videos/myvideo.mp4
```

- Check that the video runs properly:

    - The video opens properly
  
    - It plays smoothly

    - Sound comes through the correct output

    - Full screen works (press F)

----
## Media Player options

EXAMPLE:

```
vlc --fullscreen --loop /home/hackspace/Desktop/videos/myvideo.mp4
```

- FULLSCREEN : --fullscreen

- LOOP : --loop 

- PLAY AND EXIT : --play-and-exit

- NO AUDIO : --no-audio

- ASPECT RATIO : --aspect-ratio=16:9

- HIDE MOUSE : --mouse-hide-timeout=0


To see more options, explore:
 
```
vlc --help
```

----
## Run video at Start-up

- Create a startup script:

```
nano /home/hackspace/Desktop/videos/playvideo.sh
```

- Inside the file, type:

```
#!/bin/bash

# Tell X commands which display to use
export DISPLAY=:0

# Prevent screen blanking
xset s off
xset -dpms
xset s noblank

# Start shutdown timer in the background (6 hours = 21600 seconds)
(
  sleep 21600
  sudo shutdown -h now
) &


# Give the desktop time to settle
sleep 10

# Play the video
cvlc --fullscreen --loop --no-video-title-show /home/hackspace/Desktop/videos/myvideo.mp4
```

- To save and exit: CTRL + X, then Y, then Enter

- The previous script performs:

    - Play video at fullcreen and looping
 
    - Disable any screen saver, preventing the screen going to blank
 
    - Shutdown the RPi after 6 hrs of video running
 
- Now, make your file executable (permission to run the .sh script):

```
chmod +x /home/hackspace/Desktop/videos/playvideo.sh
```

- Test .sh file

```
/home/hackspace/Desktop/videos/playvideo.sh
```

- What should happen:

  - After ~10 seconds, VLC opens

  - The video plays fullscreen

  - It loops
 
- Add the script to startup

```
nano /home/hackspace/.config/autostart/playvideo.desktop
```

- A new file will open. Add the following to play video at startup:

```
[Desktop Entry]
Type=Application
Name=Play Startup Video
Exec=/home/hackspace/Desktop/videos/playvideo.sh
X-GNOME-Autostart-enabled=true
```

- Save and exit: CTRL + X, then Y, then Enter
  
- Reboot to test

- Your video should automatically run after reboot.

- Allow shutdown without password:

```
sudo nano /etc/sudoers.d/autoshutdown
```

- Add:

```
hackspace ALL=(ALL) NOPASSWD: /sbin/shutdown
```

- Save and exit: CTRL + X, then Y, then Enter

- The RPi should now shutdown after 6hrs playing the video. However, if you want to turn the RPi on again (for example, for an everyday display exhibition), you will need to do this manually. This can be:

    - Manually unplug and replugg the RPi
 
    - Power your Rpi through a *timer plug* (Reference image [here])

  
