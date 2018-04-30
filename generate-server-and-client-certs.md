# Generate Server and Client Certs

In this labs you will use cfssl to generate client and server TLS certs.

## Generate the kube-apiserver server cert

### node0




###Generate Server and Client Certs

SSL Certificates(https://cloud.google.com/compute/docs/load-balancing/http/ssl-certificates)

gcloud auth login

A login link will be generated for you in the SSH, click on it, it will require you to login with the gmail account that owns the project. A code will be generated for you after login, copy and paste it back in your SSH terminal on the line where you have

Generate the API server private key and TLS cert

sudo gcloud compute ssl-certificates create apiserver \
     --certificate apiserver.crt \
     --private-key apiserver.pem


gcloud compute ssl-certificates describe apiserver

Generate the API server private key and TLS cert

sudo gcloud compute ssl-certificates create admin \
     --certificate apiserver.crt \
     --private-key apiserver.pem
     --profile client







