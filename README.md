# bayacker

Dockerfile collection

## docker

containers

    $ docker ps
    $ docker ps -a

images

    $ docker images
    $ docker images -a

## delete all

delete containers first

    $ docker ps -aq | xargs docker rm

delete images

    $ docker images -aq | xargs docker rmi

leave tagged images.
add `-f` to force delete

    $ docker images -aq | xargs docker rmi -f

## build

    $ vi Dockerfile
    $ docker build -t bayashi/bayacker .

without build cache

    $ docker build --no-cache -t bayahi/bayacker .

## run

    $ docker run -t bayashi/bayacker
    [root@ee0a6c51e176 /]# 

## dockerhub

    $ docker login
    $ docker push bayashi/bayacker:latest
