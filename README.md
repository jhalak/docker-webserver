# Docker Development Webserver
Docker setup for creating multiple web application in single host machine with named host for faster development.

In a fresh PC we need to install many things to run multiple PHP applications. To make the things easier,
this repository consists of the most used docker images that are combined together to make multiple web applications
up and running with a less amount of time.

### Steps
* Install docker and docker-compose
* Clone this repo
* Open `docker-compose.yml` with any editor
* Add a new container info in 'Custom applications' section or modify the existing containers info
* Remove the sections that are not necessary.
* Provide the IP address of a container in `ipv4_address` attribute of `networks`.
* Save the file
* Go to cloned directory via shell and run `docker-compose up -d`
* Add the urls in your `/etc/hosts` file that are defined in `VIRTUAL_HOST` directives.
* Browse the urls in your browser.

### Inter application browsing (from one container to another)
To reach one application from another application with named route, 
provide the named route and IP in the `extra_hosts` section.
e.g. see `sso` and `survey` section.

### Mysql host
From your host machine you can reach mysql at `127.0.0.1` as host.
e.g. From host run `mysql -h 127.0.0.1 -u root -proot`

From any docker container can reach mysql at `10.11.100.1` as host
e.g.: From container run `mysql -h 10.11.100.1 -u root -proot`

