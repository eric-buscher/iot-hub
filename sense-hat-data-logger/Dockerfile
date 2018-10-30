FROM resin/raspberrypi3-alpine-python:3

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY requirements.txt /usr/src/app/
RUN pip install --upgrade pip && \
	pip install --no-cache-dir -r requirements.txt

COPY . /usr/src/app

# Finally, start our app
ENTRYPOINT ["python"]
CMD ["/usr/src/app/Sense_Logger_Final.py"]