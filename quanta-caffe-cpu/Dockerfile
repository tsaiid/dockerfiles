FROM tsaiid/femh-ai-cpu:16.04
MAINTAINER I-Ta Tsai <itsai@gmail.com>

# opencv 3.4
WORKDIR /opt

RUN git clone -b 3.4.0 --depth 1 https://github.com/opencv/opencv.git && \
    git clone -b 3.4.0 --depth 1 https://github.com/opencv/opencv_contrib.git && \
    cd opencv && \
    mkdir build && \
    cd build && \
    cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=/usr/local -DOPENCV_EXTRA_MODULES_PATH=../../opencv_contrib/modules -DOPENCV_ENABLE_NONFREE=True .. && \
    make -j"$(nproc)" && \
    make install && \
    ldconfig && \
    cd / && rm -rf /opt/opencv /opt/opencv_contrib

# Application layer
# -- Install Application into container:
#RUN set -ex && mkdir /app

WORKDIR /app

CMD ["/bin/bash"]
