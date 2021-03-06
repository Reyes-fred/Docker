FROM ubuntu:16.04
MAINTAINER Alfredo Reyes "reyes-fred@hotmail.com"

RUN apt-get update && apt-get upgrade -y 
RUN apt-get install -y sudo build-essential cmake pkg-config libjpeg8-dev \
    libtiff5-dev libjasper-dev libpng12-dev libavcodec-dev libavformat-dev \
    libswscale-dev libv4l-dev libxvidcore-dev libx264-dev \
    libatlas-base-dev gfortran wget unzip python-dev python-numpy \
    libtbb2 libtbb-dev libjpeg-dev libpng-dev libjasper-dev libdc1394-22-dev \
    libgtk-3-dev python2.7-dev python3.5-dev git python-pip python3-pip python3-testresources \
    libcanberra-gtk-module nano

RUN python -m pip install --upgrade pip && pip3 install numpy

RUN wget -O opencv3.zip https://github.com/Itseez/opencv/archive/3.4.2.zip && \
    unzip -q opencv3.zip && mv /opencv-3.4.2 /opencv

RUN wget -O opencv_contrib3.zip https://github.com/Itseez/opencv_contrib/archive/3.4.2.zip && \
    unzip -q opencv_contrib3.zip && mv /opencv_contrib-3.4.2 /opencv_contrib

RUN mkdir /opencv/build

WORKDIR "/opencv/build"

RUN  cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D BUILD_PYTHON_SUPPORT=ON \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D INSTALL_PYTHON_EXAMPLES=ON \
    -D INSTALL_C_EXAMPLES=OFF \
    -D OPENCV_EXTRA_MODULES_PATH=/opencv_contrib/modules \
    -D PYTHON3_EXECUTABLE=/usr/bin/python3.5 \
    -D BUILD_EXAMPLES=ON \
    -D BUILD_NEW_PYTHON_SUPPORT=ON \ 
    -D WITH_V4L=ON \
    -D WITH_GSTREAMER=ON \
    -D WITH_FFMPEG=ON ..

RUN make -j4 && make install && ldconfig

RUN rm -rf opencv_contrib3.zip opencv3.zip ~/opencv-3.4.2

WORKDIR "/"

RUN git clone https://github.com/Reyes-fred/Xiaomin.git

WORKDIR /Xiaomin

RUN cd Setup/ && sh setup.sh

RUN pip install imutils




