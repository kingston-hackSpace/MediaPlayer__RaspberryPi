# MediaPlayer__RaspberryPi
Run a video on start-up on a raspberry pi and screen

----
# Set up your Raspberry Pi from scratch

If you have a brand new Raspberry Pi, you will need to start installing the Operating System (OS) and initial setting. Follow [this tutorial](https://github.com/kingston-hackSpace/RaspberryPi/blob/main/How_To_SetUp_Your_RPi_From_Scratch.md)

If your Rpi already has its OS install, please skip this step. 

----
# A SCREEN FOR THE RPI

There are different screen options for your Rpi, depending on your project goals. 

- Any screen via HDMI, see settings here
 
- Embedded touch screen 7', see settings here

- Embedded touch screen (small)

- Micro OLED screen

----
# Video formats

Compatible video formats:

  - .mp4

  - .mov

  - .mkv

Recommended:

  - .mp4

  - Video codec: H.264 (AVC)

  - Audio codec: AAC

  - Resolution: up to 1920×1080

  - Frame rate: 24–30 fps

Avoid:

  - 4K videos

  - 60 fps videos

  - MPEG-2
    
----
# INSTALL VLC software

- Turn on your Rpi

- Your Rpi must be connected to Ethernet or WIFI ()

- On the Desktop, create a folder called *videos*

- Using a USB stick, copy your videos into this folder. Keep a short name for your videos.

- Open the terminal and install VLC software by typing:

  ```
  sudo apt update
  sudo apt install vlc -y
  ```

----
# TEST your video on the RPi

- Check that the video file exists:

  ```
  ls /home/hackspace/Desktop/videos
  ```

- Test the video using VLC:

  ```
  vlc /home/hackspace/Desktop/videos/myvideo.mov
  ```

- Check that the video runs properly:

    - The video opens properly
  
    - It plays smoothly

    - Sound comes through the correct output

    - Full screen works (press F)

----
# Media Player options

EXAMPLE:

```
vlc --fullscreen --loop /home/hackspace/Desktop/videos/myvideo.mov
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

