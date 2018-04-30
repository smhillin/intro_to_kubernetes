# Install and configure the Docker

In this lab you will install and configure Docker on node0 and node1.

## Configure the Docker Engine

### node0

```
gcloud compute ssh node0
```

### Install Docker

```
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh
```

### Create and Configure the docker systemd unit file

Configure the docker unit file

Most current Linux distributions (RHEL, CentOS, Fedora, Ubuntu 16.04 and higher) use systemd to manage which services start when the system boots. Ubuntu 14.10 and below use upstart.


Set the `--bip` flag to `10.200.0.1/24`:

```
sed -i -e "s/BRIDGE_IP/10.200.0.1\/24/g;" docker.service
```


Start docker:

```
sudo systemctl daemon-reload
sudo systemctl enable docker
sudo systemctl start docker
```

#### Verify

```
ip addr show docker0
sudo docker version
```


### node1

```
gcloud compute ssh node0
```

### Install Docker

```
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh
```

### Create and Configure the docker systemd unit file

Configure the docker unit file

Most current Linux distributions (RHEL, CentOS, Fedora, Ubuntu 16.04 and higher) use systemd to manage which services start when the system boots. Ubuntu 14.10 and below use upstart.


Set the `--bip` flag to `10.200.0.1/24`:

```
sed -i -e "s/BRIDGE_IP/10.200.0.1\/24/g;" docker.service
```


Start docker:

```
sudo systemctl daemon-reload
sudo systemctl enable docker
sudo systemctl start docker
```

#### Verify

```
ip addr show docker0
```

```
sudo docker version
```