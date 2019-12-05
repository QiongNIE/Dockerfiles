FROM QiongNIE/dev-env:basic

ENV DEBIAN_FRONTEND noninteractive 

RUN aptitude update && aptitude upgrade -y

RUN aptitude install -y libeigen3-dev lsb-core

# ROS
RUN sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list' && \
    apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654 && \
    curl -sSL 'http://keyserver.ubuntu.com/pks/lookup?op=get&search=0xC1CF6E31E6BADE8868B172B4F42ED6FBAB17C654' | apt-key add -  && \
    aptitude update && \
    aptitude install -y ros-melodic-desktop-full && \
    aptitude install -y ros-melodic-map-server

RUN echo "source /opt/ros/melodic/setup.zsh" >> ~/.zshrc 


# glog
RUN git clone  https://github.com/gflags/gflags.git && \ 
    cd gflags && \
    mkdir build && \
    cd build && \
    cmake -DBUILD_SHARED_LIBS=ON  ..  && \
    make  && \
    make install && \
    cd ../.. && rm -r gflags && \
    git clone https://github.com/google/glog.git && \
    cd glog && \
    mkdir build && \
    cd build && \
    cmake -DBUILD_SHARED_LIBS=ON  .. && \
    make && \
    make install && \
    cd ../.. && rm -r glog


# opencv
RUN aptitude update && aptitude install -y software-properties-common && \
    add-apt-repository "deb http://security.ubuntu.com/ubuntu xenial-security main" && \
    aptitude update && \
    aptitude install -y libjasper1 libjasper-dev libgtk-3-dev libatlas-base-dev liblapacke-dev && \
    aptitude clean

RUN cd /home/ && \
    git clone https://github.com/opencv/opencv.git && \
    git clone https://github.com/opencv/opencv_contrib.git
# COPY opencv.zip /home/opencv.zip
# COPY opencv_contrib.zip /home/opencv_contrib.zip

RUN /opt/conda/bin/conda uninstall -y libtiff &&  /opt/conda/bin/conda install -y hdf5
# RUN cd /home/ && unzip opencv.zip &&  unzip opencv_contrib.zip 
RUN cd /home/opencv && mkdir build && cd build && \
    cmake -D CMAKE_BUILD_TYPE=Release \
    -D CMAKE_INSTALL_PREFIX=/usr/local/opencv \
    -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules \
    -D INSTALL_C_EXAMPLES=OFF \
    -D INSTALL_PYTHON_EXAMPLES=OFF \
    -D BUILD_EXAMPLES=OFF \
    -D WITH_CUDA=ON \
    -D WITH_TBB=ON \
    -D OPENCV_ENABLE_NONFREE=ON \
    -D WITH_OPENGL=ON \
    -D WITH_OPENMP=ON \
    -D BUILD_opencv_world=ON  \
    -D CUDA_ARCH_BIN=6.1 7.0 \
    ..
#    make -j4 && \
#    make install && \
#    ldconfig

#RUN cd /home/ && \
    # rm opencv.zip && \
    # rm opencv_contrib.zip && \
#    rm -r  opencv && \
#    rm -r opencv_contrib








