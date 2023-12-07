FROM node:14 as builder

USER root
ARG PIA_VERSION=3.2.2
ARG NODE_SASS_VERSION=4.14.1
ARG ANGULAR_CLI_VERSION=11.0.1

WORKDIR /build

RUN npm install -g @angular/cli@$ANGULAR_CLI_VERSION

RUN wget https://github.com/LINCnil/pia/archive/refs/tags/v$PIA_VERSI>

RUN unzip v$PIA_VERSION.zip \
    && rm v$PIA_VERSION.zip \
    && cd pia-$PIA_VERSION \
    # Note, it should be npm ci but the upstream do not necessarily s>
    && npm install \
    && npm install node-sass@$NODE_SASS_VERSION \
    && ng build --prod --build-optimizer && ls -la \
     && mv dist/pia-angular /tmp/pia  && ls /tmp && ls /tmp/pia

FROM nginx:latest

RUN mkdir -p /var/www && chown www-data. /var/www/

COPY ./conf/cnil_pia.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /tmp/pia /var/www/
