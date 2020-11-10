# docker build command 
sudo docker build -t fr/l4t-ml:1.0 .

# run docker command
sudo docker run -it --rm --net=host --runtime nvidia  --device /dev/i2c-1 -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix fr/l4t-ml:1.0


