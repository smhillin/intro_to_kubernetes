# Install GCE client tools

## Install the Google 'gcloud' SDK

Follow the instructions [here](https://cloud.google.com/sdk/) to install gcloud.
Then, set the Google Cloud project that you want to use for this lab as the default, by running:

```
gcloud config set project <your-project-id>
gcloud config set compute/zone us-central1-f
gcloud config set compute/region us-central1
```

Note: if you don't yet have a Google Cloud project created, then follow the signup
instructions [here](https://cloud.google.com/compute/docs/signup).

Grab the service account docs from here:

[Google Service Account Docs](https://developers.google.com/console/help/new/#serviceaccounts)

## Verify your account is setup correctly

Run the following commands to make sure your GCE account is setup:

Create a VM named `workshop-test`

```
gcloud compute instances create kub-test \
 --image-project ubuntu-os-cloud \
 --image-family ubuntu-1604-lts \
 --boot-disk-size 200GB \
 --machine-type n1-standard-1 \
 --can-ip-forward \
 --scopes compute-rw
```


List all VMs:

```
gcloud compute instances list
```

SSH into Kub-Test

```
gcloud compute ssh kub-test
```

Delete the `kub-test` VM:

```
exit kub-test
gcloud compute instances delete kub-test
```
