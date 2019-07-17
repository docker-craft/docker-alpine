FROM docker.repo/alpine-base:3.9.4

# Here we install GNU libc (aka glibc) and set C.UTF-8 locale as default.

RUN GLIBC_BASE_URL="https://github.com/sgerrand/alpine-pkg-glibc/releases/download" && \
    GLIBC_PACKAGE_VERSION="2.29-r0" && \
    GLIBC_BASE_PACKAGE_FILENAME="glibc-$GLIBC_PACKAGE_VERSION.apk" && \
    GLIBC_BIN_PACKAGE_FILENAME="glibc-bin-$GLIBC_PACKAGE_VERSION.apk" && \
    GLIBC_I18N_PACKAGE_FILENAME="glibc-i18n-$GLIBC_PACKAGE_VERSION.apk" && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget \
        "$GLIBC_BASE_URL/$GLIBC_PACKAGE_VERSION/$GLIBC_BASE_PACKAGE_FILENAME" \
        "$GLIBC_BASE_URL/$GLIBC_PACKAGE_VERSION/$GLIBC_BIN_PACKAGE_FILENAME" \
        "$GLIBC_BASE_URL/$GLIBC_PACKAGE_VERSION/$GLIBC_I18N_PACKAGE_FILENAME" && \
    apk add --no-cache \
        "$GLIBC_BASE_PACKAGE_FILENAME" \
        "$GLIBC_BIN_PACKAGE_FILENAME" \
        "$GLIBC_I18N_PACKAGE_FILENAME" && \
    \
    rm "/etc/apk/keys/sgerrand.rsa.pub" && \
    /usr/glibc-compat/bin/localedef --force --inputfile POSIX --charmap UTF-8 C.UTF-8 || true && \
    echo "export LANG=C.UTF-8" > /etc/profile.d/locale.sh && \
    \
    apk del glibc-i18n && \
    rm \
        "$GLIBC_BASE_PACKAGE_FILENAME" \
        "$GLIBC_BIN_PACKAGE_FILENAME" \
        "$GLIBC_I18N_PACKAGE_FILENAME"

ENV LANG=C.UTF-8
