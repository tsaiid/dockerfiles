help:
	@cat Makefile

IMAGE=tsaiid/femh-ai-gpu:ssd
DOCKER_FILE=Dockerfile
GPU?=1
DOCKER=GPU=$(GPU) nvidia-docker
APP=/home/tsaiid/git/femh-dicom
DATA=/home/data

build:
	docker build -t $(IMAGE) -f $(DOCKER_FILE) .

bash: build
	$(DOCKER) run -it -v $(APP):/app -v $(DATA):/data --net=host $(IMAGE)
