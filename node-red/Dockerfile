# base-image for node on any machine using a template variable,
# see more about dockerfile templates here:http://docs.resin.io/pages/deployment/docker-templates
# Note the node:slim image doesn't have node-gyp
FROM resin/raspberrypi3-node:6.10.3

# Defines our working directory in container
RUN mkdir -p /usr/src/app/
WORKDIR /usr/src/app

# Install node modules, including i2c-bus without carrying all the deps in the layers
RUN JOBS=MAX npm install -g node-sense-hat node-red node-red-contrib-resinio --production --silent && \
	npm cache clean --force && rm -rf /tmp/*

# This will copy all files in our root to the working  directory in the container
COPY ./app ./

ENTRYPOINT ["/sbin/tini","--"]

# Enable systemd init system in container
# ENV INITSYSTEM=on

# server.js will run when container starts up on the device
CMD ["/usr/src/app/start.sh"]
