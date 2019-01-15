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
## Setup Kubernetes, Pull Image and Run
https://cloud.google.com/kubernetes-engine/docs/quickstart

### Create New Google Cloud Kubernetes Cluster (Only need if not done yet, better to create on Google Console, creating on command line creates expensive cluster by default)
```
gcloud config set project irwsdsqufgdx
```
```
gcloud config set compute/zone asia-southeast1-b	
```
```
gcloud container clusters create upbiz-standard-cluster
````
### Setup Google Cloud Kubernetes credentials
```
gcloud container clusters get-credentials upbiz-standard-cluster
```

Run the image in Kubernetes
```
kubectl run upbiz-prisma-server --image gcr.io/irwsdsqufgdx/upbiz-prisma-img --port 4466
```
Passing in --type LoadBalancer creates load balancer.  Need load balancer to get external IP address.
```
kubectl expose deployment upbiz-prisma-server --type LoadBalancer --port 4466 --target-port 4466
```
Inspect server
```
kubectl get service upbiz-prisma-server
```
View service
```
http://[EXTERNAL_IP]/
```
### Remove service
```
kubectl delete service upbiz-prisma-server
```
Delete deployment
```
kubectl delete deployment <deployment name>
````
### Delete Cluster (Dangerous, only if want to take down service permanently)
```
gcloud container clusters delete upbiz-standard-cluster
```
