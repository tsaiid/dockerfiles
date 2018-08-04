FROM tsaiid/keras
MAINTAINER I-Ta Tsai <itsai@gmail.com>

RUN pip install --upgrade pip && \
    pip install \
      scikit-image \
      imgaug \
      opencv-python && \
    conda clean -yt

WORKDIR /app

EXPOSE 8888

#CMD bash

