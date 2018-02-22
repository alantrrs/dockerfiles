ARG cuda_version=9.1-devel
FROM nvidia/cudagl:${cuda_version}

WORKDIR /bullet3

# Install dependencies
RUN apt update && apt install -y git cmake ffmpeg pkg-config qtbase5-dev libqt5opengl5-dev libassimp-dev libpython3.5-dev libboost-python-dev libtinyxml-dev

# Install bullet3
RUN git clone https://github.com/bulletphysics/bullet3 /bullet3 && \
  bash ./build_cmake_pybullet_double.sh
RUN cd build_cmake && make install
RUN export PYTHONPATH=/bullet3/build_cmake/examples/pybullet
