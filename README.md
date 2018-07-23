# Exercise 1 [ Part B ] - Prometheus & Grafana docker-compose stack

An EC2 instance of type t2.micro based on a Ubuntu image .
A Loadbalancer forwarding incoming requests to the EC2 instance

## Pre-requisites

Before we get started installing the Prometheus stack. Ensure you install the latest version of docker and docker swarm on your Docker host machine. Docker Swarm is installed automatically when using Docker for Mac or Docker for Windows.

## Installation & Configuration

If you would like to change which targets should be monitored or make configuration changes edit the /prometheus/prometheus.yml file

The targets section is where you define what should be monitored by Prometheus. The names defined in this file are actually sourced from the service name in the docker-compose file. If you wish to change names of the services you can add the "container_name" parameter in the docker-compose.yml file.

Once configurations are done let's start it up. From the /prometheus project directory run the following command:

$ HOSTNAME=$(hostname) docker stack deploy -c docker-compose.yml prom

That's it the `docker stack deploy' command deploys the entire Grafana and Prometheus stack automagically to the Docker Swarm. By default cAdvisor and node-exporter are set to Global deployment which means they will propogate to every docker host attached to the Swarm.

The Grafana Dashboard is now accessible via: http://<Host IP Address>:3000

username - admin
password - foobar

In order to check the status of the newly created stack:

$ docker stack ps prom

View running services:

$ docker service ls

View logs for a specific service

$ docker service logs prom_<service_name>


