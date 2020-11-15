# mask_camera
"mask_camera" is identify put on mask or not and simply measure temperature using USB camera and IR array sensor on NVIDIA Jetson device.

# DEMO


# Features


# Requirement
NVIDIA Jetson device
USB camera (Logcool 270)
IR array sensor

# Installation

# Usage
## docker build command
'''
$ sudo docker build -t fr/l4t-ml:1.0 .
'''
## docker run command
'''
$ sudo docker run -it --rm --net=host --runtime nvidia  --device /dev/i2c-1 -e DISPLAY=$DISPLAY -v ~/src/mask_camera/src/:/root/src -v /tmp/.X11-unix/:/tmp/.X11-unix fr/l4t-ml:1.0
'''

how to verify i2c device on docker container
use i2cdetect command then response as below should be fine.
'''
\# i2cdetect -r -y 1
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- 68 -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- --
'''

# Note

# Author
