# Docker Compose

Prepare for the demo:

* Prune the docker system on manager
* Clean up the images

Execute:

```
docker swarm leave --force
docker system prune --force
docker rmi webapp dbapp
```

* Go to /vagrant/app

## Explore the app source code

```
less websvc/app.py
less websvc/Dockerfile
less web-compose.yml
```

## Building and running the web app

```
docker-compose -f web-compose.yml build
docker-compose -f web-compose.yml up
```

In another window execute

```
docker ps
docker network ls
curl http://127.0.0.1:3000/
curl http://127.0.0.1:3000/db
```

### Logging

* Inspect the error logs
* Stop the app
* Restart the app as a daemon

Execute:

```
docker-compose -f web-compose.yml up -d
```

* Repeat the CURL requests
* Inspect the compose logs

Execute:

```
docker-compose -f web-compose.yml logs
```

### Cleanup

```
docker-compose -f web-compose.yml down
```

## Building and running the app stack

```
less stack-compose.yml
docker-compose -f stack-compose.yml build
docker-compose -f stack-compose.yml up
```

* Cleanup: inspect stopped containers, cleanup

Note: the containers used in a compose stack are not removed when the stack is stopped, but when you execute **docker-compose down**.

Execute:

```
docker ps -a
docker-compose -f stack-compose.yml down --volumes
docker ps -a
```

## Run Netbox

```
cd ~/netbox-docker/
docker-compose up -d
docker-compose port nginx 8080
```

* Connect to http://192.168.33.2:<port>/

Cleanup:

```
docker ps -a
docker-compose stop
docker ps -a
docker-compose down
docker volume ls
docker-compose down --volumes
```