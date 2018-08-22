help:
	@cat Makefile

IMAGE=tsaiid/chexnet
DATA?=/home/data
GPU?=1
DOCKER_FILE=Dockerfile
DOCKER=GPU=$(GPU) nvidia-docker
BACKEND=tensorflow
PYTHON_VERSION?=3.6
CUDA_VERSION?=9.0
CUDNN_VERSION?=7
TEST=tests/
SRC?=$(shell dirname `pwd`)

build:
	docker build -t $(IMAGE) -f $(DOCKER_FILE) .

bash: build
	$(DOCKER) run -it \
		-v $(SRC):/src/workspace \
		-v $(DATA):/data \
		-v /home/tsaiid/git/CheXNet-Keras:/app \
		--net=host --env KERAS_BACKEND=$(BACKEND) $(IMAGE) bash
