FROM tsaiid/femh-ai-cpu:16.04
MAINTAINER I-Ta Tsai <itsai@gmail.com>

RUN apt-get update && apt-get install -y \
        dcmtk && \
    rm -rf /usr/share/docs && rm -rf /usr/share/man && \
    rm -rf /var/lib/apt/lists/*

# Application layer
# -- Install Application into container:
WORKDIR /app

RUN git clone -b v0.1.1 --depth 1 https://github.com/tsaiid/femh-dicom.git . && \
    pip3 install -r requirements.txt

COPY config/cxr-20180906.yml config/cxr.yml
COPY models models

RUN groupadd -g 1000 appuser && \
    useradd -r -u 1000 -g appuser appuser && \
    mkdir /dcm_tmpdir && \
    chown -R 1000:1000 /dcm_tmpdir
USER appuser

CMD ["sh", "/app/workflow/hourly-classification.sh"]
