FROM docker.repo/alpine-openjdk:8u212

LABEL maintainer="Ming Chen<uchenm@gmail.com>"

RUN apk update && apk add --no-cache git zip unzip openssh-client subversion

CMD ["mvn"]

ENV MAVEN_HOME /opt/maven

RUN set -o errexit -o nounset \
    && echo "Adding maven user and maven" \
    && addgroup -g 1000 -S maven  \
    && adduser  maven -u 1000 -D -S -s /bin/bash -G maven -h /home/maven \
    && mkdir /home/maven/.m2 \
    && chown --recursive maven:maven /home/maven \
    \
    && echo "Symlinking root maven cache to gradle maven cache" \
    && ln -s /home/maven/.m2 /root/.m2

VOLUME /home/maven/.m2

WORKDIR /home/maven

ENV MAVEN_VERSION=3.6.1
ARG MAVEN_DOWNLOAD_SHA256=51169366d7269ed316bad013d9cbfebe3a4ef1fda393ac4982d6dbc9af2d5cc359ee12838b8041cb998f236486e988b9c05372f4fdb29a96c1139f63c991e90e
ENV BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries
RUN set -o errexit -o nounset \
    && echo "Downloading Maven" \
    && wget --no-verbose --output-document=maven.zip ${BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.zip \
    \
    && echo "Checking download hash" \
    && echo "${MAVEN_DOWNLOAD_SHA256} *maven.zip" | sha512sum --check - \
    \
    && echo "Installing maven" \
    && unzip maven.zip \
    && rm maven.zip \
    && mv "apache-maven-${MAVEN_VERSION}" "${MAVEN_HOME}/" \
    && ln --symbolic "${MAVEN_HOME}/bin/mvn" /usr/bin/mvn \
    \
    && echo "Testing MAVEN installation" \
    && mvn --version
