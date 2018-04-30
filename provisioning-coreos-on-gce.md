# Provisioning Ubuntu on Google Compute Engine

In this lab you will provision two GCE instances running Ubuntu.

## Provision 2 GCE instances

### Provision Ubuntu using the gcloud CLI


### node0

```
gcloud compute instances create node0 \
 --image-project ubuntu-os-cloud \
 --image-family ubuntu-1604-lts \
 --boot-disk-size 200GB \
 --machine-type n1-standard-1 \
 --can-ip-forward 
```

### node1

```
gcloud compute instances create node1 \
 --image-project ubuntu-os-cloud \
 --image-family ubuntu-1604-lts \
 --boot-disk-size 200GB \
 --machine-type n1-standard-1 \
 --can-ip-forward 
```

#### Verify

```
gcloud compute instances list
```
