# Now Prisma

## Deploy

```
$ now RyukyuInteractive/now-prisma
```

or

```
$ now
```
# Kubernetes Setup and Deploy
## Build the docker image and Push onto Registry
Reference: https://cloud.google.com/container-registry/docs/quickstart
### Build docker image
Open the upbiz-express source code
```
docker-compose build
```
### Set Google Docker Registry for Development Pushing, and Deployment Pulling
1. Get authentication info for docker
```
gcloud auth configure-docker
```
2. Setup registry location and tag the image
(Project ID: irwsdsqufgdx)
```
docker tag upbiz-prisma-img gcr.io/irwsdsqufgdx/upbiz-prisma-img
```
If don't specify "tag1" then default will use "latest".
3. Push the image onto the registry
```
docker push gcr.io/irwsdsqufgdx/upbiz-prisma-img
```
4. Pulling the image on another computer
```
docker pull gcr.io/irwsdsqufgdx/upbiz-prisma-img
```
