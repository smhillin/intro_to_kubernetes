# Scale-Up-Simple-Example

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

