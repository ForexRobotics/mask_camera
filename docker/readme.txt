# docker build command 
$ sudo docker build -t fr/l4t-ml:1.0 .

# run docker command
$ sudo docker run -it --rm --net=host --runtime nvidia --privileged --device /dev/video0 --device /dev/i2c-1 -e DISPLAY=$DISPLAY -v ~/src/mask_camera/src/:/root/src -v /tmp/.X11-unix/:/tmp/.X11-unix fr/l4t-ml:1.0
