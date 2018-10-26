# base-image for node on any machine using a template variable,
# see more about dockerfile templates here:http://docs.resin.io/pages/deployment/docker-templates
# Note the node:slim image doesn't have node-gyp
FROM resin/raspberrypi3-alpine-node:8-slim

# Defines our working directory in container
RUN mkdir -p /usr/src/app/ && mkdir -p /usr/share/doc/python-rpi.gpio
WORKDIR /usr/src/app

# Install node modules, including i2c-bus without carrying all the deps in the layers
RUN apk add --update --upgrade --no-cache libevdev-dev linux-headers make musl-dev gcc g++ py-numpy-dev python && \
  npm -g install --update --upgrade npm && \
  JOBS=MAX npm install -g --update --upgrade bcrypt node-sense-hat node-red node-red-contrib-resinio \
  node-red-contrib-cast node-red-contrib-google-iot-core node-red-node-pi-sense-hat --production --silent && \
  apk del libevdev-dev linux-headers make musl-dev gcc g++ && \
  npm cache clean --force && rm -rf /tmp/*

# This will copy all files in our root to the working  directory in the container
COPY ./app ./

ENTRYPOINT ["/sbin/tini", "--"]

# server.js will run when container starts up on the device
CMD ["bash", "/usr/src/app/start.sh"]