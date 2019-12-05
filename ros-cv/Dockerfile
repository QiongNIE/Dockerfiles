FROM QiongNIE/dev-env:ros-cv-cache

RUN aptitude update && aptitude upgrade -y

RUN cd /home/opencv/build && \
    make -j4 && \
    make install && \
    ldconfig

RUN cd /home/ && \
    rm -r  opencv && \
    rm -r opencv_contrib

COPY conda_env_torch1.3_cv4.yaml /home/conda_env_torch1.3_cv4.yaml
RUN /opt/conda/bin/conda env create -f /home/conda_env_torch1.3_cv4.yaml && rm /home/conda_env_torch1.3_cv4.yaml

RUN cd /home/ && \
    wget https://download.jetbrains.com/cpp/CLion-2019.2.5.tar.gz && \
    tar zfx CLion-2019.2.5.tar.gz && \
    rm CLion-2019.2.5.tar.gz










