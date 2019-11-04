FROM docker.repo.io/alpine:3.10

COPY repositories /etc/apk/repositories

RUN apk update && apk add --no-cache bash gawk sed grep bc coreutils ca-certificates wget unzip zip git openssh-client 


