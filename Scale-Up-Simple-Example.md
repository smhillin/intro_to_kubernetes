# Scale-Up-Simple-App

You add more replicas to your application's Deployment resource by using the kubectl scale command. To add two additional replicas to your Deployment (for a total of three), run the following command:
```
	kubectl scale deployment hello-web --replicas=3
```

You can see the new replicas running
```
	kubectl get deployment hello-web


	kubectl get pods
```
Now, you have multiple instances of your application running independently of each other and you can use the kubectl scale command to adjust capacity of your application.


# Cleanup(Only if this is your last lab)

First check to see your deployments are showing

```
	kubectl get deployments
```

Delete deployments.  This delete automatically propogates to any under lying pods oand replicasets.
```
	kubectl delete deployment/hello-web

```
Check to make sure deployments are deleted

```
	kubectl get deployments
```

Check to make sure deployments propogated to pods.


```
	kubectl get pods
```


Check to verify your 3 k8 nodes are running.

```
	kubectl get pods
```
