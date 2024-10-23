.PHONY: build img

IMGNAME := xss_wordpress_demo
PORT := 8050

all : build

build:
        docker build -t $(IMGNAME):latest -f Dockerfile .

start: build
        docker run --rm -it -p $(PORT):80 $(IMGNAME)

background:
        docker run --rm -d -p $(PORT):80 $(IMGNAME)

shell:
        docker exec -it $(shell docker ps | grep $(IMGNAME) | awk '{split($$0,a," "); print a[1]}') bash

stop:
        docker stop $(shell docker ps | grep $(IMGNAME) | awk '{split($$0,a," "); print a[1]}')
