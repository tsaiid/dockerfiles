help:
	@cat Makefile

CURR_DATE=$(shell date +'%Y%m%d')
IMAGE=tsaiid/femh-hourly-classification
DOCKER_FILE=Dockerfile
SRC=/Users/tsaiid/git/femh-dicom

build:
	docker build -t $(IMAGE):$(CURR_DATE) -f $(DOCKER_FILE) .

build-test:
	docker build -t $(IMAGE):test -f $(DOCKER_FILE) .

test:
	docker run -it --rm -e TZ=Asia/Taipei -p 11112:11112 $(IMAGE):test

bash:
	docker run -it --rm -e TZ=Asia/Taipei -p 11112:11112 $(IMAGE):$(CURR_DATE) bash

bash-test:
	docker run -it --rm -e TZ=Asia/Taipei -p 11112:11112 $(IMAGE):test bash
#	docker run -it --rm -e TZ=Asia/Taipei -P $(IMAGE):test bash

bash-test-local: build-test
	docker run -it --rm -e TZ=Asia/Taipei $(IMAGE):test bash
