# auto-scale-deployement






Create a simple deployment


Create a Horizontal Pod Autoscaler for that deployment


## CPU Based Scaling
```
kubectl autoscale deployment <deployment-name> --min=1 --max=5 --cpu-percent=80

kubectl get hpa
```


Update existing minimum or maximum number of replicas by creating a yaml file and updating settings.


```

kubectl get hpa/tomcat02 -o yaml > tomcat-hpa.yaml

nano tomcat-hpa.yaml

```

Save the yaml file and then apply changes.


```
kubectl apply -f tomcat-hpa.yaml

```

Check to see the status of your HPA

```

kubectl get HPA


```