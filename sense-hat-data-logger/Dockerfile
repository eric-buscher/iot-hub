FROM resin/raspberrypi3-alpine-python:3.6

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY requirements.txt /usr/src/app/
RUN pip install --upgrade pip && \
	pip install --no-cache-dir -r requirements.txt

COPY sense-hat-data-logger.py /usr/src/app

ENTRYPOINT ["/sbin/tini", "--"]
CMD ["/usr/local/bin/python","/usr/src/app/sense-hat-data-logger.py"]