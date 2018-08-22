help:
	@cat Makefile

IMAGE=tsaiid/cx_oracle:16.04
DOCKER_FILE=Dockerfile

build:
	docker build -t $(IMAGE) -f $(DOCKER_FILE) .

bash: build
	$(DOCKER) run -it -v $(SRC):/src/workspace -v $(DATA):/data -v /home/tsaiid/git/CheXNet-Keras:/app --net=host --env KERAS_BACKEND=$(BACKEND) $(IMAGE) bash
