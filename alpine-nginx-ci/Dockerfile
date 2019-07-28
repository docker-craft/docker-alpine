FROM docker.repo.io/alpine-nginx:1.17.2

LABEL maintainer="Ming Chen<uchenm@gmail.com>"

COPY --chown=root:root nginx.conf /etc/nginx/
COPY --chown=root:root conf.d/*.conf /etc/nginx/conf.d/
COPY --chown=root:root index.html /usr/share/nginx/html/
