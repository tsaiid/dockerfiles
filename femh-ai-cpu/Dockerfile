FROM tsaiid/cx_oracle:16.04
MAINTAINER I-Ta Tsai <itsai@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        wget \
        libatlas-base-dev \
        libboost-all-dev \
        libgflags-dev \
        libgoogle-glog-dev \
        libhdf5-serial-dev \
        libleveldb-dev \
        liblmdb-dev \
        libopencv-dev \
        libprotobuf-dev \
        libsnappy-dev \
        protobuf-compiler \
        python3-dev \
		dcmtk && \
    rm -rf /var/lib/apt/lists/*

# python packages
RUN python3 -m pip install --upgrade pip && \
	pip3 install cx_Oracle sqlalchemy \
				 pydicom deid \
				 opencv-python pillow \
			     numpy scipy pandas \
				 tqdm \
				 tensorflow keras \
				 flask flask_sqlalchemy

ENV CAFFE_ROOT=/opt/caffe
ENV PYCAFFE_ROOT $CAFFE_ROOT/python
ENV PYTHONPATH $PYCAFFE_ROOT:$PYTHONPATH
ENV PATH $CAFFE_ROOT/build/tools:$PYCAFFE_ROOT:$PATH

WORKDIR $CAFFE_ROOT

RUN git clone -b 1.0 --depth 1 https://github.com/BVLC/caffe.git . && \
    cd python && for req in $(cat requirements.txt) pydot; do pip install $req; done && cd .. && \
    mkdir build && cd build && \
    cmake -DCPU_ONLY=1 -Dpython_version=3 .. && \
    make -j"$(nproc)" && \
    echo "$CAFFE_ROOT/build/lib" >> /etc/ld.so.conf.d/caffe.conf && ldconfig && \
    apt-get -y autoremove && apt-get clean

#RUN git clone -b master --depth 1 https://github.com/intel/caffe.git . && \
#    for req in $(cat python/requirements.txt) pydot; do pip install $req; done && \
#    mkdir build && cd build && \
#    cmake -DCPU_ONLY=1 -DUSE_MLSL=1 -DCMAKE_BUILD_TYPE=Release -Dpython_version=3 .. && \
#    make all -j"$(nproc)" && \
#    echo "$CAFFE_ROOT/build/lib" >> /etc/ld.so.conf.d/caffe.conf && ldconfig && \
#    apt-get -y autoremove && apt-get clean

# pynetdicom3
WORKDIR /opt/pynetdicom3

RUN git clone --depth 1 https://github.com/pydicom/pynetdicom3.git . && \
	python3 setup.py install && \
    cd / && rm -rf /opt/pynetdicom3

# Application layer
# -- Install Application into container:
#RUN set -ex && mkdir /app

WORKDIR /app

CMD ["/bin/bash"]
