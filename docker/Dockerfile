# Docker file required NVIDIA l4t tensorflow2.3 keras opencv
# base image
FROM nvcr.io/nvidia/l4t-tensorflow:r32.4.4-tf2.3-py3
# maintainer
MAINTAINER Kaz TAKAHASHI <ktakahashi@forexrobotics.jp>
# update modules
RUN apt update && apt upgrade -y
# install modules
RUN apt install -y \
	curl \
	vim \
	git \
	zip \
	cmake \
	libopencv-dev \
	python3-opencv
# install python library
RUN pip3 install keras pillow adafruit-circuitpython-amg88xx Jetson.GPIO matplotlib

