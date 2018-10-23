# base-image for node on any machine using a template variable,
# see more about dockerfile templates here:http://docs.resin.io/pages/deployment/docker-templates
# Note the node:slim image doesn't have node-gyp
FROM resin/raspberrypi3-node:8-slim

# Defines our working directory in container
RUN mkdir -p /usr/src/app/
WORKDIR /usr/src/app

# Install node modules, including i2c-bus without carrying all the deps in the layers
RUN npm cache verify && \
    rm -rf /usr/local/lib/node_modules && \
	rm -rf /usr/local/bin/node && \
	rm -rf /usr/local/bin/npm && \
	apt-get update && \
	apt-get autoremove --purge &&\
	apt-get update && apt-get install -yq --no-install-recommends \
		curl && \
	apt-get clean && rm -rf /var/lib/apt/lists/*

RUN ( curl -sL https://raw.githubusercontent.com/node-red/raspbian-deb-package/master/resources/update-nodejs-and-nodered ) | /bin/sh -c --

RUN JOBS=MAX npm install -g --production --unsafe-perm \
       	node-sense-hat && \
		node-red-contrib-resinio && \
	npm cache clean --force && \
	rm -rf /tmp/*

# This will copy all files in our root to the working  directory in the container
COPY ./app ./

ENTRYPOINT ["/sbin/tini","-c","--"]

# Enable systemd init system in container
# ENV INITSYSTEM=on

# server.js will run when container starts up on the device
CMD ["/bin/bash", "/usr/src/app/start.sh"]
