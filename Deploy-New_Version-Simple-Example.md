# Deploy-New_Version-Simple-Example


## Create Rolling Update for v2 of Hello World

Kubernetes Engine's rolling update mechanism ensures that your application remains up and available even as the system replaces instances of your old container image with your new one across all the running replicas.

You can create an image for the v2 version of your application by building the same source code and tagging it as v2 (or you can change the "Hello, World!" string to "Hello, Kubernetes Engine!" before building the image):

```

	cd /Users/Shaun/kubernetes-engine-samples/hello-app

	nano main.go

	docker build -t gcr.io/${PROJECT_ID}/hello-app:v2 .
```

Now, apply a rolling update to the existing deployment with an image update:

```
	kubectl set image deployment/hello-web hello-web=gcr.io/${PROJECT_ID}/hello-app:v2
```

View your pods.  You can see the new update rolling. 

```
	gcloud compute instances list

```

#Cleaning up

```
Delete the Service

	kubectl delete service hello-web

Delete the Container Cluster


	gcloud container clusters delete hello-cluster in us-central1-b


```

