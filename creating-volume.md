# Creating Volumes


### Create new pod with shared volume



Use a repo to create a new pod with shared colume

```
	kubectl create -f https://raw.githubusercontent.com/mhausenblas/kbe/master/specs/volumes/pod.yaml


	kubectl describe pod sharevol
```

Exec into one of the containers c1
```
	kubectl exec sharevol -c c1 -i -t -- bash
```
Use these bash commands to mount the shared volume
```
	mount | grep xchange
```
Save some data to volume
```
	echo 'some data' > /tmp/xchange/data
```
Exit the container and exec into the second container
```
	kubectl exec sharevol -c c2 -i -t -- bash
```
Mount the Volume and see if you can read from the shared volume
```
	mount | grep /tmp/data

	cat /tmp/data/data
```


### Cleanup

```

Delete all pods and volumes

	kubectl delete po,svc --all

```