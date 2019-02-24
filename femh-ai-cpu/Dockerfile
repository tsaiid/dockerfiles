FROM tsaiid/cx_oracle:16.04
MAINTAINER I-Ta Tsai <itsai@gmail.com>

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        git \
        wget \
        python3-dev \
        dcmtk && \
    rm -rf /var/lib/apt/lists/*

# python packages
RUN python3 -m pip install --upgrade pip && \
    pip3 install cx_Oracle sqlalchemy \
                 pydicom pynetdicom \
                 opencv-python pillow \
                 numpy scipy pandas \
                 tqdm \
                 tensorflow keras \
                 flask flask_sqlalchemy

# Application layer
# -- Install Application into container:
#RUN set -ex && mkdir /app

WORKDIR /app

CMD ["/bin/bash"]
