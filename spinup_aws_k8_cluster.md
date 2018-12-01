This lab should be run on Ubuntu 16.04.

## Install Kubernetes and Docker on All Nodes

`
sudo su
`

### Check for current instalation of Docker

`
Docker version
`

### Uninstall Current Version(if installed)

`
sudo apt-get remove docker docker-engine docker.io
`

### Update and upgrade the apt-get package manager

`
apt-get update && apt-get upgrade && sudo apt-get install -y apt-transport-https
`

### Check for available versions in Docker repo

`
apt-cache madison docker-ce
`

### Add Docker Secure Key

`
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
`


### If no previous versions of docker available Add Docker Repo

`
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
`

### Update Package Manager

`
apt-get update
`

### Check for version 18.03.1 (this is the latest version that will work with kubeadmin)

`
apt-cache madison docker-ce
`

### Install Docker

`
apt-get install docker-ce=18.03.1~ce-0~ubuntu
`

### Start and enable docker engine
`
systemctl start docker
systemctl enable docker
`

### Download and add the key to Kubernetes install

`
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add
`

### Add the package to apt-get

`
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >> /etc/apt/sources.list.d/kubernetes.list
`

### Apt-get update and install Kubernetes

`
apt-get update && apt-get install -y kubelet kubeadm kubectl kubernetes-cni
`


## Master Node Initialization


### Sign as root

`
sudo su -
`

### Pass bridged IPv4 traffic to iptables` chains which is required by certain CNI networks

`
sysctl net.bridge.bridge-nf-call-iptables=1
`

### Initialize kubeadm (done only for master)

`
kubeadm init --pod-network-cidr=10.244.0.0/16
`

After running the command above you should recieve a succes message 

"Your Kubernetes master has initialized successfully!"

You will also see snippet code with the format below

"sudo kubeadm join --token <token> <IP>:6443 --discovery-token-ca-cert-hash
<hash>"

Copy this code you will need it later to add worker nodes to the cluster.



### Create kubeconfig so the user can run kubectl commands

`
mkdir -p $HOME/.kube
`

`
cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
`

`
chown $(id -u):$(id -g) $HOME/.kube/config
`

### Install flannel networking to allow linux nodes to communicate
`
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/v0.9.1/Documentation/kube-flannel.yml
`

### Only when you want to use master node to host pods 

`
kubectl taint nodes --all node-role.kubernetes.io/master-
`

### Test

`
kubectl get pods --all-namespaces
`

## Worker Node Initialization

Run the commands below on all the worker nodes after installing Docker and Kubernetes.

### Sign in as Root

`
sudo su
`

### Pass bridged IPv4 traffic to iptables` chains which is required by certain CNI networks

`
sysctl net.bridge.bridge-nf-call-iptables=1
`

### Get the token that you copied from step 3 above and run in the new node

"sudo kubeadm join --token <token> <IP>:6443 --discovery-token-ca-cert-hash
<hash>"

If you don't have the informaiton you can run the follwoing code on the master

`
kubeadm  token create --print-join-command
`

### Test

Return to master node and run the below command to see if worker nodes have joined cluster 

`
kubectl get nodes
`


 

