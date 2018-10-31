FROM resin/raspberrypi3-alpine-node:slim

# Defines our working directory in container
VOLUME /data
WORKDIR /usr/src/app

# Install node modules, including i2c-bus without carrying all the deps in the layers
RUN apk add --no-cache make gcc g++ python && \
  JOBS=MAX npm install -g node-red node-red-contrib-resinio --production --silent && \
  apk del make gcc g++ python && \
  npm cache clean --force && rm -rf /tmp/*

# This will copy all files in our root to the working  directory in the container
COPY ../../../node-red .

ENV DBUS_SYSTEM_BUS_ADDRESS=unix:path/=//host//run//dbus//system_bus_socket

# Make the default flows available in the user library
RUN mkdir -p /data/node-red/user/lib/flows || true && \
	cp /usr/src/app/flows/* /data/node-red/user/lib/flows/

ENV INITSYSTEM on
RUN rc-update add root boot
RUN rc-update add procfs boot
RUN rc-update add mtab boot
RUN rc-update add fsck boot
RUN rc-update add swap boot
RUN rc-update add udev sysinit
RUN /etc/TZ > /etc/timezone
RUN mkdir -p /etc/env.d
RUN echo 'XSESSION="Xfce4"' > /etc/env.d/90xsession
RUN echo 'EDITOR="/usr/bin/nano"' > /etc/env.d/90xsession
RUN reboot

ENTRYPOINT ["/usr/bin/entry.sh"]
# server.js will run when container starts up on the device
CMD ["node-red-pi","--settings","/usr/src/app/settings.js"]