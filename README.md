# DEMO
[![mask camera demo](https://img.youtube.com/vi/-wq80_ZY_kQ/0.jpg)](https://www.youtube.com/watch?v=-wq80_ZY_kQ)

## Youtube Link
https://youtu.be/-wq80_ZY_kQ

# Features
The mask_camera project uses the NVIDIA Jetson Development Kit series and WebCam to determine whether a mask can be worn. In addition, by connecting an IR array sensor device called AMG8833 as an option, the surface temperature of the human body can be measured at the same time.
![Nobody](https://user-images.githubusercontent.com/26875192/99191269-116c4380-27af-11eb-8a3a-64c328fe7965.png)
![Masked](https://user-images.githubusercontent.com/26875192/99191484-504ec900-27b0-11eb-8a1a-94f66b0eba52.png)
![Unmasked](https://user-images.githubusercontent.com/26875192/99190624-dc5df200-27aa-11eb-86e6-3f98e8ac83fd.png)
The operating environment can be operated on the docker container with TensorFlow2 and Keras installed, and the learning model can be replaced with the one created independently on the TeachableMachine site.

# Story
Since COVID-19, the importance of wearing masks and measuring temperature has increased worldwide. However, the current situation is that dedicated camera devices are expensive and do not reach the people who need them. The purpose of this project is to contribute to the "democratization of AI" by providing open source solutions using inexpensive and high-speed AI edge devices such as NVIDIA Jetson Nano.

# Requirement
- NVIDIA Jetson device (veirfied on Jetson Nano 2GB)

- Logcool 270 (USB Camera) 
https://www.amazon.com/Logitech-C270-720pixels-Black-webcam/dp/B01BGBJ8Y0/ref=sr_1_3?dchild=1&keywords=C270&qid=1605453031&sr=8-3
- Optional: AMG8833 (IR array sensor)
https://www.sparkfun.com/products/14607

# setup hardware
AMG8833 is an optional sensor device for this project.
When you connect AMG8833 to Jetson, you will see the  tempreture in the video frame.

## connection AMG8833 - Jetson
The connection between AMG8833 and Jetson is as follows.
```
AMG8833(3.3V) ⇔ GPIO1(3.3V)
AMG8833(GND) ⇔ GPIO6(Ground)
AMG8833(SDA) ⇔ GPIO3(SDA)
AMG8833(SCL) ⇔ GPIO5(SCL)
```
![pins](https://user-images.githubusercontent.com/26875192/99191849-e126a400-27b2-11eb-8c2f-ff16fa5eae26.png)


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
## Pin to WebCam
Fix AMG8833 so that the field of view is about the same as WebCam.
![camera](https://user-images.githubusercontent.com/26875192/99191984-99ece300-27b3-11eb-8e35-a246970b934e.png)


# Installation
## clone gituhub and build docker container
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


# Issues & FAQ
## Issues
- IR thermal sensor measures just surface temperature. You can change TEMP_CARIBRATION and TEMP_THRESHOLD caribration value and threshold in mask_camera.py.

## FAQ
- [Q] Poped up Low memory resource alert. 
- [A] Please close another window and reduce other memory usage especially Jetson Nano 2GB is low main memory resource.

# Author
Kazuyuki TAKAHASHI Forex Robotics CO., Ltd.
<takahashi@forexrobotics.jp>