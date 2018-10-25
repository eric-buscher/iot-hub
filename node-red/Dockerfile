# base-image for node on any machine using a template variable,
# see more about dockerfile templates here:http://docs.resin.io/pages/deployment/docker-templates
# Note the node:slim image doesn't have node-gyp
FROM resin/raspberrypi3-alpine-node:8

EXPOSE 1880

# Defines our working directory in container
RUN mkdir -p /usr/src/app/
WORKDIR /usr/src/app

RUN export DBUS_SYSTEM_BUS_ADDRESS=unix:path=/host/run/dbus/system_bus_socket

# Install node modules, including i2c-bus without carrying all the deps in the layers
RUN apk add --no-cache --update --upgrade --virtual node-build-deps \
		build-base \
    	make \
    	gcc \
    	g++ \
    	libgcc \
    	libstdc++ \
    	libuv \
    	libcrypto1.0 \
    	libssl1.0 \
    	linux-headers \
        linux-rpi-dev \
    	musl-dev \
    	musl-utils \
    	python-dev && \
    npm install npm && \
	JOBS=MAX npm update -g \
		node-pre-gyp \
		rpio \
	    rpi-gpio \
		node-sense-hat \
		node-red \
	    node-red-contrib-resinio \
	    node-red-node-pi-sense-hat \
    --production && \
	apk del \
		node-build-deps && \
	npm cache clean --force && \
		rm -rf /tmp/*

#Add the current user to the gpio group to access the nrgpio script for interacting with the gpio pins
RUN addgroup $USER gpio

# This will copy all files in our root to the working  directory in the container
COPY ./app ./

# Make the default flows available in the user library
RUN mkdir -p /data/node-red/user/lib/flows || true
RUN cp /usr/src/app/flows/* /data/node-red/user/lib/flows/

# server.js will run when container starts up on the device
CMD ["node-red-pi","--max-old-space-size=256"]
