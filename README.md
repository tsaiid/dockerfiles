# Dockerfile

- tsaiid/ubuntu-py3:16.04
    - tsaiid/cx_oracle:16.04
        - tsaiid/femh-ai-cpu:16.04
            - tsaiid/femh-hourly-classification:16.04
            - tsaiid/quanta-caffe-cpu:16.04
    - tsaiid/keras-tf-cpu
- nvidia/cuda
    - tsaiid/keras
        - tsaiid/chexnet
    - tsaiid/femh-ai-gpu
    - tsaiid/caffe-py3-gpu
- ubuntu:16.04
    - tsaiid/caffe-py3-cpu:16.04
