FROM QiongNIE/dev-env:ros-cv

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y libatlas-base-dev libeigen3-dev libsuitesparse-dev

RUN git clone --depth=1 -b 1.14.0 https://ceres-solver.googlesource.com/ceres-solver

RUN cd ./ceres-solver && mkdir ceres-bin && cd ceres-bin && cmake .. && make -j3 && make install


