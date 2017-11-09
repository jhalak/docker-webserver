# Docker Development Webserver for Laravel application
Docker setup for creating multiple laravel application in single host machine with named host for faster development.

In a fresh PC we need to install many things to run multiple PHP applications. To make the things easier,
this repository consists of the most used docker images that are combined together to make multiple laravel applications
up and running with a less amount of time.

### Steps
* Install docker and docker-compose
* Clone this repo
* Copy `docker-compose.yml.sample` to `docker-compose.yml`. (`cp docker-compose.yml.sample docker-compose.yml)
* Open `docker-compose.yml` with any editor
* Add a new container info in 'Custom applications' section or modify the existing containers info
* Remove the sections that are not necessary.
* Provide the IP address of a container in `ipv4_address` attribute of `networks`.
* Create a directory anywhere to store the data of your various databases. e.g. `/opt/data` and create 5 directories in that is described in `volumes` properties of `data` section. Then change the mapping so that the left side of `:` part matches all the directories. e.g.
```
- /path/to/your-data-directory/mysql:/var/lib/mysql
- /path/to/your-data-directory/postgres:/var/lib/postgres
- /path/to/your-data-directory/mariadb:/var/lib/mariadb
- /path/to/your-data-directory/redis:/var/lib/redis
- /path/to/your-data-directory/memcached:/var/lib/memcached
```
* Save the file
* Copy `start.sh.sample` to `start.sh`. (`cp start.sh.sample start.sh`)
* Open `start.sh` and change the 4th line so that it meets your custom application names.
* Go to the root of the cloned repo and run `./start.sh`.
* Add the urls in your `/etc/hosts` file that are defined in `VIRTUAL_HOST` directives.
* Browse the urls in your browser.

### Inter application browsing (from one container to another)
To reach one application from another application with named route,
provide the named route and IP in the `extra_hosts` section.
e.g. see `sso` and `laravel54` section.

### Mysql host
From your host machine you can reach mysql at `127.0.0.1` as host.
e.g. From host run `mysql -h 127.0.0.1 -u root -proot`

From any docker container can reach mysql at `10.11.100.1` as host
e.g.: From container run `mysql -h 10.11.100.1 -u root -proot`
