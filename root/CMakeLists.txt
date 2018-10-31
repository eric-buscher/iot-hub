# cmake_minimum_required(VERSION <specify CMake version here>)
project(.)

set(CMAKE_CXX_STANDARD 14)

add_executable(.
		../etc/conf.d/hwclock
		../etc/env.d/99editor
		../etc/rc.conf
		.dockerignore
		docker-compose.yml
		Dockerfile
		iot_hub.iml
		../usr/src/node-red/assets/favicon.ico
		../usr/src/node-red/assets/resin.css
		../usr/src/node-red/assets/resin_logo.png
		../usr/src/node-red/flows/resin.json
		../usr/src/node-red/.dockerignore
		../usr/src/node-red/Dockerfile
		../usr/src/node-red/LICENCE
		../usr/src/node-red/node-red.iml
		../usr/src/node-red/README.md
		../usr/src/node-red/settings.js
		../usr/src/sense-hat-data-logger/.dockerignore
		../usr/src/sense-hat-data-logger/__init__.py
		../usr/src/sense-hat-data-logger/Dockerfile
		../usr/src/sense-hat-data-logger/requirements.txt
		../usr/src/sense-hat-data-logger/sense-hat-data-logger.iml
		../usr/src/sense-hat-data-logger/sense-hat-data-logger.py
		../usr/src/sense-hat-data-logger/sense-hat-data-logger.service
		../.gitignore)
