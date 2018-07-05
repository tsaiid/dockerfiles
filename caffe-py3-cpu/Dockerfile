#FROM ubuntu:18.04
FROM ubuntu:16.04
MAINTAINER I-Ta Tsai <itsai@gmail.com>

# Oracle Instant Client layer
COPY instantclient/* /tmp/

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
		alien \
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
		dcmtk \
		libaio1 \
		python3 \
        python3-dev \
        python3-pip \
        python3-setuptools && \
    alien -iv /tmp/oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm && \
    alien -iv /tmp/oracle-instantclient12.2-devel-12.2.0.1.0-1.x86_64.rpm && \
    rm -rf /var/lib/apt/lists/*

# Environment variables
ENV ORACLE_HOME=/usr/lib/oracle/12.2/client64
ENV LD_LIBRARY_PATH=$ORACLE_HOME/lib
ENV PATH=$ORACLE_HOME/bin:$PATH
ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8

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
WORKDIR $CAFFE_ROOT

# FIXME: use ARG instead of ENV once DockerHub supports this
# https://github.com/docker/hub-feedback/issues/460
ENV CLONE_TAG=1.0

RUN git clone -b ${CLONE_TAG} --depth 1 https://github.com/BVLC/caffe.git . && \
    cd python && for req in $(cat requirements.txt) pydot 'python-dateutil>2'; do pip3 install $req; done && cd .. && \
    mkdir build && cd build && \
    cmake -DCPU_ONLY=1 -Dpython_version=3 .. && \
    make -j"$(nproc)"

ENV PYCAFFE_ROOT $CAFFE_ROOT/python
ENV PYTHONPATH $PYCAFFE_ROOT:$PYTHONPATH
ENV PATH $CAFFE_ROOT/build/tools:$PYCAFFE_ROOT:$PATH
RUN echo "$CAFFE_ROOT/build/lib" >> /etc/ld.so.conf.d/caffe.conf && ldconfig

# pynetdicom3
ENV PYNETDICOM_ROOT=/opt/pynetdicom3
WORKDIR $PYNETDICOM_ROOT

RUN git clone --depth 1 https://github.com/pydicom/pynetdicom3.git . && \
    #cd pynetdicom3 && \
	python3 setup.py install

# Clean
#RUN apt-get -y autoremove && apt-get clean && \
#    apt-get purge -y alien perl perl5 && apt-get -y autoremove && apt-get clean && \
#    rm -rf /usr/share/doc && rm -rf /usr/share/man

# Application layer
# -- Install Application into container:
RUN set -ex && mkdir /app

WORKDIR /app

CMD ["/bin/bash"]
