include ../../.env
export $(shell sed 's/=.*//' ../../.env)

REGISTRY=$(AWS_ACCOUNT_ID).dkr.ecr.$(AWS_REGION).amazonaws.com

clean:
	rm -rf common

build:
	mkdir -p common/
	rsync -av ../common/* common/
	docker build -t $(ECS_SELENIUM_FIREFOX_IMAGE) --build-arg VERSION=latest .
	rm -rf common/

tag: build
	docker tag $(ECS_SELENIUM_FIREFOX_IMAGE) $(REGISTRY)/$(ECS_SELENIUM_FIREFOX_IMAGE):latest

push: tag
	docker push $(REGISTRY)/$(ECS_SELENIUM_FIREFOX_IMAGE):latest
