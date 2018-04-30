# Deploy-New-Version-Simple-App


## Create New Docker Image 

Kubernetes Engine's rolling update mechanism ensures that your application remains up and available even as the system replaces instances of your old container image with your new one across all the running replicas.

You can create an image for the v2 version of your application by building the same source code and tagging it as v2 (or you can change the "Hello, World!" string to "Hello, Kubernetes Engine!" before building the image):

```

	nano main.go

	docker build -t gcr.io/${PROJECT_ID}/hello-app:v2 .
```

## Apply Rolling Update

Now, apply a rolling update to the existing deployment with an image update:

```
	kubectl set image deployment/hello-web hello-web=gcr.io/${PROJECT_ID}/hello-app:v2
```

View your pods.  You can see the new update rolling. 

```
	kubectl get pods

```

# Cleaning up


Delete the Service

```
	kubectl get services

	kubectl delete service hello-web

```

Delete the deployments and it will propgate and delete all the pods

```
	kubectl get deployments

	kubectl delete deployments/hello-web
```



