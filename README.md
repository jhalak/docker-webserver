# Docker Development Webserver
Docker setup for creating multiple web application in single host machine with named host for faster development.

In a fresh PC we need to install many things to run multiple PHP applications. To make the things easier, 
this repository consists of the most used docker images that are combined together to make multiple web applications
up and running with a less amount of time.

###Steps
* Install docker and docker-compose
* Clone this repo
* Add a new container info in 'Custom applicaitons' section or modify the existing container info
* Run docker-compose up -d
* Add the urls in your /ets/hosts file that are defined in 'VIRTUAL_HOST' directives.
* Browse the urls in your browser.
