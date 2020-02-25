FROM node:10.19-jessie

WORKDIR "/application"

# Fix debconf warnings upon build
ARG DEBIAN_FRONTEND=noninteractive

RUN npm install -g pm2
RUN yarn policies set-version $YARN_VERSION

RUN npm install --global gulp-cli

USER node

EXPOSE 3030 3003 3017 3018 3019
