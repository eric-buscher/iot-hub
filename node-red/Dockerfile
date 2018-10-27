FROM resin/raspberrypi3-alpine-node:slim

# Defines our working directory in container
VOLUME /usr/src/app/
WORKDIR /usr/src/app

# Install node modules, including i2c-bus without carrying all the deps in the layers
RUN apk add --no-cache make gcc g++ python && \
  JOBS=MAX npm install -g node-red node-red-contrib-resinio --production --silent && \
  apk del make gcc g++ python && \
  npm cache clean --force && rm -rf /tmp/*

# This will copy all files in our root to the working  directory in the container
COPY ./app ./

ENV DBUS_SYSTEM_BUS_ADDRESS=unix:path/=//host//run//dbus//system_bus_socket

# Make the default flows available in the user library
RUN mkdir -p /data/node-red/user/lib/flows || true && \
	cp /usr/src/app/flows/* /data/node-red/user/lib/flows/

# server.js will run when container starts up on the device
CMD ["node-red-pi","--settings","/usr/src/app/settings.js"]