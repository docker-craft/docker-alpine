FROM docker.repo/alpine-openjdk:8u212

LABEL maintainer="Ming Chen<uchenm@gmail.com>"

RUN apk update && apk add --no-cache git zip unzip openssh-client subversion

CMD ["gradle"]

ENV GRADLE_HOME /opt/gradle

    #&& groupadd --system --gid 1000 gradle \
    #&& useradd --system --gid gradle --uid 1000 --shell /bin/bash --create-home gradle \
RUN set -o errexit -o nounset \
    && echo "Adding gradle user and group" \
    && addgroup -g 1000 -S gradle  \
    && adduser  gradle -u 1000 -D -S -s /bin/bash -G gradle -h /home/gradle \
    && mkdir /home/gradle/.gradle \
    && chown --recursive gradle:gradle /home/gradle \
    \
    && echo "Symlinking root Gradle cache to gradle Gradle cache" \
    && ln -s /home/gradle/.gradle /root/.gradle

VOLUME /home/gradle/.gradle

WORKDIR /home/gradle


ENV GRADLE_VERSION 5.5.1
ARG GRADLE_DOWNLOAD_SHA256=222a03fcf2fcaf3691767ce9549f78ebd4a77e73f9e23a396899fb70b420cd00
RUN set -o errexit -o nounset \
    && echo "Downloading Gradle" \
    && wget --no-verbose --output-document=gradle.zip "https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip" \
    \
    && echo "Checking download hash" \
    && echo "${GRADLE_DOWNLOAD_SHA256} *gradle.zip" | sha256sum --check - \
    \
    && echo "Installing Gradle" \
    && unzip gradle.zip \
    && rm gradle.zip \
    && mv "gradle-${GRADLE_VERSION}" "${GRADLE_HOME}/" \
    && ln --symbolic "${GRADLE_HOME}/bin/gradle" /usr/bin/gradle \
    \
    && echo "Testing Gradle installation" \
    && gradle --version