# base-image for node on any machine using a template variable,
# see more about dockerfile templates here:http://docs.resin.io/pages/deployment/docker-templates
# Note the node:slim image doesn't have node-gyp
FROM resin/raspberrypi3-node:6.10.3

EXPOSE 80

# Defines our working directory in container
RUN mkdir -p /usr/src/app/
WORKDIR /usr/src/app

RUN export DBUS_SYSTEM_BUS_ADDRESS=unix:path=/host/run/dbus/system_bus_socket

# Install node modules, including i2c-bus without carrying all the deps in the layers
RUN JOBS=MAX npm install -g node-sense-hat node-red-pi node-red-contrib-resinio --production && \
	npm cache clean --force && rm -rf /tmp/*

# This will copy all files in our root to the working  directory in the container
COPY ./app ./

# Make the default flows available in the user library
RUN mkdir -p /data/node-red/user/lib/flows || true
RUN cp /usr/src/app/flows/* /data/node-red/user/lib/flows/

# Enable tini init system in container
ENTRYPOINT ["/sbin/tini","--"]

# server.js will run when container starts up on the device
CMD ["node-red-pi","--settings","/usr/src/app/settings.js"]
