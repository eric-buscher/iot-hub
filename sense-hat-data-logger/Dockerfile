FROM resin/raspberrypi3-alpine-python:2.7-slim

RUN apk add --no-cache \
	    python2 && \
	python2 -m ensurepip && \
	rm -r /usr/lib/python*/ensurepip && \
	pip install --upgrade \
		pip && \
	pip install --upgrade \
		wheel \
		evdev \
		pillow \
		sense-hat \
		sense-hat-display-utils \
		threading2 && \
	rm -r /root/.cache

COPY . /usr/src/app
RUN mkdir -p /usr/var/log
WORKDIR /usr/var/log

# Finally, start our app
CMD ["python2", "/usr/src/app/Sense_Logger_Final.py"]