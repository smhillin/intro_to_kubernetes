

## Install Kubernetes and Docker on All Nodes(Skip if already Installed)


### Update and upgrade the apt-get package manager
`
sudo apt-get update && sudo apt-get upgrade && sudo apt-get install -y apt-transport-https


### Install Docker

`
sudo apt-get install docker-ce=18.03.1~ce~3-0~ubuntu
`

### Start and enable docker engine
`
sudo systemctl start docker
sudo systemctl enable docker
`

### Download and add the key to Kubernetes install

`
sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add
`

### Add the package to apt-get

`
echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >> /etc/apt/sources.list.d/kubernetes.list
`

### Apt-get update and install Kubernetes

`
sudo apt-get update && sudo apt-get install -y kubelet kubeadm kubectl kubernetes-cni
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

sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config

sudo chown $(id -u):$(id -g) $HOME/.kube/config
`

### Install flannel networking
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

Run the commands below on all the worker nodes.

### Sign in as Root

`
sudo su
`

### Pass bridged IPv4 traffic to iptables` chains which is required by certain CNI networks

`
sudo sysctl net.bridge.bridge-nf-call-iptables=1
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


 

