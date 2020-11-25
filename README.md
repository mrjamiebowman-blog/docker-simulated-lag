# Docker Container: "Simulated Lag" (tc, socat)
This docker container can act as a proxy to route traffic to another destination while simulating lag. This is great for building grafana dashboards locally and verifying that the metrics appear to be correct for monitoring http latency.

## Blog Post
[Simulating Lag with Docker Containers](https://www.mrjamiebowman.com/devops/docker-devops/simulating-lag-with-docker-containers/)

## How to use
You'll have to modify the startup.sh script.

Change `connect` to the name of the docker container that you want to reroute traffic to.

`DESTINATION_IP=$(dig connect +short)`

Change the port (8083) to reroute traffic to the correct port. This was used for Kafka Connect API so 80 or 443 could work as well.

`socat tcp-listen:8083,reuseaddr,fork tcp:$DESTINATION_IP:8083`