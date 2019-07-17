FROM docker.repo/alpine:3.9.4

COPY repositories /etc/apk/repositories

RUN apk update && apk add --no-cache bash gawk sed grep bc coreutils ca-certificates wget


