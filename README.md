# DEMO
[![mask camera demo](https://img.youtube.com/vi/-wq80_ZY_kQ/0.jpg)](https://www.youtube.com/watch?v=-wq80_ZY_kQ)

https://youtu.be/-wq80_ZY_kQ

# Features

![Nobody](https://user-images.githubusercontent.com/26875192/99191269-116c4380-27af-11eb-8a3a-64c328fe7965.png)
![Masked](https://user-images.githubusercontent.com/26875192/99191484-504ec900-27b0-11eb-8a1a-94f66b0eba52.png)
![Unmasked](https://user-images.githubusercontent.com/26875192/99190624-dc5df200-27aa-11eb-86e6-3f98e8ac83fd.png)

# Requirement
- NVIDIA Jetson device (veirfied on Jetson Nano 2GB)

- Logcool 270 (USB Camera) 
https://www.amazon.com/Logitech-C270-720pixels-Black-webcam/dp/B01BGBJ8Y0/ref=sr_1_3?dchild=1&keywords=C270&qid=1605453031&sr=8-3
- Optional: AMG8833 (IR array sensor)
https://www.sparkfun.com/products/14607

# Installation
## docker build command
```
$ git clone https://github.com/ForexRobotics/mask_camera.git

$ cd docker

$ sudo docker build -t fr/l4t-ml:1.0 .
```
## run docker container and program
```
$ cd docker

$ sudo docker run -it --rm --net=host --runtime nvidia --privileged --device /dev/video0 --device /dev/i2c-1 -e DISPLAY=$DISPLAY -v ~/src/mask_camera/src/:/root/src -v /tmp/.X11-unix/:/tmp/.X11-unix fr/l4t-ml:1.0

# cd /root/src

# python3 mask_camera.py
```

## exit program
enter [q] key on video frame window or ctrl + [c] key on docker console then exit program.

## connection AMG8833 - Jetson
```
AMG8833(3.3V) ⇔ GPIO1(3.3V)
AMG8833(GND) ⇔ GPIO6(Ground)
AMG8833(SDA) ⇔ GPIO3(SDA)
AMG8833(SCL) ⇔ GPIO5(SCL)
```

## veirfy sensor connction
how to verify i2c device on docker container
use i2cdetect command then response as below should be fine.
```
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
```

# FAQ
- [Q] Poped up Low memory resource alert. 
- [A] Please close another window and reduce other memory usage especially Jetson Nano 2GB is low main memory resource.

# Author
Kazuyuki TAKAHASHI Forex Robotics CO., Ltd.
<takahashi@forexrobotics.jp>