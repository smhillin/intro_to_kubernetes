# Kubernetes Simple App Deployment



## Install Docker CE and GIT on your work station

```
choose instructions for respective machine(https://docs.docker.com/install/)


choose instructions for respective machine(https://git-scm.com/downloads)

```


## Build the container image


For this tutorial, you will deploy a sample web application called hello-app, a web server written in Go that responds to all requests with the message “Hello, World!” on port 80.

To download the hello-app source code, run the following commands:

```
	git clone https://github.com/GoogleCloudPlatform/kubernetes-engine-samples

	cd kubernetes-engine-samples/hello-app
```

Set the PROJECT_ID environment variable in your shell by retrieving the pre- configured project ID on gcloud by running the command below:
```
	export PROJECT_ID="$(gcloud config get-value project -q)"
```

The value of PROJECT_ID will be used to tag the container image for pushing it to your private Container Registry.

To build the container image of this application and tag it for uploading, run the following command:
```
	docker build -t gcr.io/${PROJECT_ID}/hello-app:v1 .
```

This command instructs Docker to build the image using the Dockerfile in the current directory and tag it with a name, such as gcr.io/my-project/hello-app:v1. The gcr.io prefix refers to Google Container Registry, where the image will be hosted. Running this command does not upload the image yet.


View your local docker images.
```
	docker images
```
## Upload the container image

```
	gcloud docker -- push gcr.io/${PROJECT_ID}/hello-app:v1
```
## Test the container image locally

```
	docker run --rm -p 8080:8080 gcr.io/${PROJECT_ID}/hello-app:v1

	curl http://localhost:8080
```


## Create a container cluster

Now that the container image is stored in a registry, you need to create a container cluster to run the container image. A cluster consists of a pool of Compute Engine VM instances running Kubernetes, the open source cluster orchestration system that powers Kubernetes Engine.

Run the following command to create a three-node cluster named hello-cluster:

```
	gcloud container clusters create hello-cluster --num-nodes=3
```

It may ask you to specify a zone:
```
	gcloud config set compute/zone us-central1-b
```

It may take a few minutes to spin up your cluster.  Wait a bit and then view Your clusters.

```
	gcloud compute instances list
```

You should see your 3 nodes running


## Deploy your application

To deploy and manage applications on a Kubernetes Engine cluster, you must communicate with the Kubernetes cluster management system. You typically do this by using the kubectl command-line tool.

The kubectl run command below causes Kubernetes to create a Deployment named hello-web on your cluster. 

```
	export PROJECT_ID="$(gcloud config get-value project -q)"

	kubectl run hello-web --image=gcr.io/${PROJECT_ID}/hello-app:v1 --port 8080
```

To see the pod created

```
	kubectl get pods
```

## Expose your application to the internet

```
	kubectl expose deployment hello-web --type=LoadBalancer --port 80 --target-port 8080
```


## View live your application

View the details of your running services

```
kubectl describe services
```

Find the LoadBalancer Ingress and put the address in your browser to see your live application.

