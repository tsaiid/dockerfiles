help:
	@cat Makefile

CURR_DATE=`date +'%Y%m%d'`
IMAGE=tsaiid/femh-hourly-classification
DOCKER_FILE=Dockerfile
SRC=/home/tsaiid/git/femh-dicom
IMGSRV=/mnt/data/cxr

build:
	docker build -t $(IMAGE):$(CURR_DATE) -f $(DOCKER_FILE) .

build-test:
	docker build -t $(IMAGE):test -f $(DOCKER_FILE) .

bash: build
	docker run -it --rm -v $(SRC):/app -v $(DATA):/imgsrv -e TZ=Asia/Taipei -p 11112:11112 $(IMAGE):$(CURR_DATE) bash

bash-test: build-test
	docker run -it --rm -v $(SRC):/app -v $(DATA):/imgsrv -e TZ=Asia/Taipei -p 11112:11112 $(IMAGE):test bash

bash-test-local: build-test
	docker run -it --rm -v $(SRC):/app -v $(DATA):/imgsrv -e TZ=Asia/Taipei $(IMAGE):test bash
