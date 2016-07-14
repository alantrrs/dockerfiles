FROM alantrrs/cuda-opencv:nvidia

# Install Caffe dependencies
RUN sudo apt-get update
RUN sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libhdf5-serial-dev protobuf-compiler
RUN sudo apt-get install -y  --no-install-recommends libboost-all-dev
RUN sudo apt-get install -y libatlas-base-dev 
RUN sudo apt-get install -y libgflags-dev libgoogle-glog-dev liblmdb-dev

# Clone the Caffe repo 
RUN git clone https://github.com/BVLC/caffe.git /caffe
WORKDIR /caffe

# Use gcc 4.6 
# Fixes internal compiler error: Segmentation fault while compiling tests
#RUN sudo apt-get install -y gcc-4.6 g++-4.6 gcc-4.6-multilib g++-4.6-multilib

#RUN update-alternatives --install /usr/bin/cc cc /usr/bin/gcc-4.6 30 && \
#  update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++-4.6 30 && \ 
#  update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.6 30 && \
#  update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.6 30

# Remove ippicv because it wasn't installed with opencv
RUN sed -i 's/-lippicv//' /usr/local/lib/pkgconfig/opencv.pc 
# Build Caffe core
RUN cp Makefile.config.example Makefile.config && \ 
    echo "OPENCV_VERSION := 3" >> Makefile.config && \
    echo "USE_PKG_CONFIG := 1" >> Makefile.config && \
    sed -i 's/CXX :=/CXX ?=/' Makefile 
    # echo "CXX := /usr/bin/g++-4.6" >> Makefile.config && \
RUN make all
RUN make test

# Install python dependencies
RUN sudo apt-get install -y gfortran
RUN sudo easy_install pillow
RUN for req in $(cat python/requirements.txt); do pip install $req; done

# Numpy include path hack - github.com/BVLC/caffe/wiki/Setting-up-Caffe-on-Ubuntu-14.04
#RUN NUMPY_EGG=`ls /usr/local/lib/python2.7/dist-packages | grep -i numpy` && \
#  ln -s /usr/local/lib/python2.7/dist-packages/$NUMPY_EGG/numpy/core/include/numpy /usr/include/python2.7/numpy

# Build Caffe python bindings and make + run tests
RUN make pycaffe

# Add binaries to path
RUN echo "export PATH=/caffe/.build_release/tools:$PATH" >> ~/.bashrc


