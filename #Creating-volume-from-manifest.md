#Creating-Volumes-From-manifest



###Create a Volume from a Deployment Manifest

```


You can create a Deployment of Pod where each Pod contains one or more Volumes. The following Deployment manifest describes a Deployment of three Pods that each have an emptyDir Volume.


- The metadata: name field specifies a Deployment named volumes-example-deployment.
- The Pod template specification includes a volumes field that describes an emptyDir volume named cache-volume.
- The container specification includes a volumeMounts: field that specifies that the Volume named cache-volume is mounted at the file path /cache.


apiVersion: apps/v1beta2
kind: Deployment
metadata:
  name: volumes-example-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: demo
  template:
    metadata:
      labels:
        app: demo
    spec:
      containers:
      - name: test-container
        image: gcr.io/google-samples/hello-app:1.0
        volumeMounts:
        - mountPath: /cache
          name: cache-volume
      volumes:
        - name: cache-volume
          emptyDir: {}


Create a new file volumes-demo.yaml
	
	nano volumes-demo.yaml


To create a Deployment from this manifest file, run the following command:

	kubectl apply -f volumes-demo.yaml

Verify that your Deployment is running correctly and has the expected Volume with this command:


	kubectl describe pods volumes-example-deployment


This prints information about each of the three Pods in the Deployment. The output shows that each Pod has a container, test-container, with the /cache mount

	Mounts:
	  /cache from cache-volume (rw)

The output also slows that each Pod contains a Volume named cache-volume:

	Volumes:
  cache-volume:
    Type:    EmptyDir (a temporary directory that shares a pod's lifetime)

```



