FROM resin/raspberrypi3-alpine-python:3.6

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY requirements.txt .
RUN pip install --upgrade pip && \
	pip install --no-cache-dir -r requirements.txt

COPY sense-hat-data-logger.py /etc/init.d/sense-hat-data-logger.py
RUN export -p > /etc/saved.env && \
	chmod a+x /etc/init.d/sense-hat-data-logger.py

ENV INITSYSTEM on
COPY sense-hat-data-logger.service /etc/systemd/system/sense-hat-data-logger.service
RUN systemctl enable /etc/systemd/system/sense-hat-data-logger.service