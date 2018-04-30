# Create A Kubernetes Cluster


## install kubectl

```
	gcloud components install kubectl


	gcloud container clusters create test‐cluster
```

You may get an error message that you need to enable kubernetes API.  Paste link into your browser and enable API.


View your clusters 
```

	gcloud container clusters list

```

Delete your Clusters

```
	gcloud container clusters delete test-cluster


```