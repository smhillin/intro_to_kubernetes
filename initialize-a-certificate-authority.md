# Initialize a certificate authority

In this lab you will setup the necessary PKI infrastructure to secure the Kuberentes API for remote communication. This lab will leverage CloudFlare's PKI toolkit, [cfssl](https://github.com/cloudflare/cfssl), to bootstrap a Certificate Authority.

## Download and install cfssl

### node0

```
gcloud compute ssh node0
```



```
Generate the RSA private key

mkdir ssl_cert
 cd ssl_cert
 openssl genrsa -out apiserver.pem 2048
 ```


```
Get the PROJECT_ID:



PROJECT_ID=$(curl -H "Metadata-Flavor: Google" \
  http://metadata.google.internal/computeMetadata/v1/project/project-id)
Get the EXTERNAL_IP:

Get the EXTERNAL_IP:

EXTERNAL_IP=$(curl -H "Metadata-Flavor: Google" \
  http://metadata.google.internal/computeMetadata/v1/instance/network-interfaces/0/access-configs/0/external-ip)


${PROJECT_ID}
${EXTERNAL_IP}

```


 ```
To generate a signed certificate, you will need a certificate signing request (CSR). Run the following command to create one

 openssl req -new -key apiserver.pem -out apiserver.csr

 ```

 ```
You can use your new CSR to obtain a valid certificate from a certificate authority. Alternatively, you can generate a self-signed certificate by running the following:

 openssl x509 -req -days 365 -in apiserver.csr -signkey apiserver.pem -out apiserver.crt
 
 ```