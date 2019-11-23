#First step
Create a Docker network for the proxy to share with containers. The Docker network is necessary so that we can use it with applications that are run using Docker Compose. Let’s call this network proxy.
 - docker network create proxy

 Next, create an empty file which will hold our Let’s Encrypt information. We’ll share this into the container so Traefik can use it:
 - touch acme.json
 - chmod 600 acme.json


 Finally, create the Traefik container with this command:


docker run -d -p 8080:8080 -p 80:80 \
-v $PWD/traefik.yml:/etc/traefik/traefik.yml \
-v /var/run/docker.sock:/var/run/docker.sock \
--network proxy \
--name traefik \
traefik:v2.0
