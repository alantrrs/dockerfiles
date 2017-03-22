FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04

## Install OpenCV 3.2 last stable commit
RUN apt-get -y update
RUN apt-get -y install python-pip git nano curl tmux htop mc wget libeigen3-dev
RUN apt-get install -y build-essential cmake libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev python-dev python-numpy libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev ocl-icd-opencl-dev libcanberra-gtk3-module
RUN pip install matplotlib

RUN git clone https://github.com/Itseez/opencv.git /opencv
WORKDIR /opencv/
RUN git checkout 3.2.0

RUN mkdir /opencv/build
WORKDIR /opencv/build
RUN cmake -D CMAKE_BUILD_TYPE=RELEASE \
      -D CMAKE_INSTALL_PREFIX=/usr/local \
      -D WITH_OPENGL=ON \
      -D WITH_TBB=OFF \
      -D BUILD_opencv_world=OFF \
      -D BUILD_opencv_python2=ON \
      -D BUILD_opencv_python3=OFF \
      -D INSTALL_PYTHON_EXAMPLES=ON \
      -D WITH_V4L=ON \
      ..
RUN make -j7
RUN make install

# For some reason cv2.so doesn't get copied
RUN cp /opencv/build/lib/cv2.so /usr/local/lib/python2.7/dist-packages/

RUN ldconfig
