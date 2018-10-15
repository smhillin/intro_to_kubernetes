

# Install Kubernetes on All Nodes

## Install Package

`
apt-get update
apt-get install -y kubelet=1.11.3-00 kubeadm-1.11.3-00 kubectl
`

## Master Node

### Step 1: sign as root

`
sudo su -
`

### Step 2: pass bridged IPv4 traffic to iptables` chains which is required by certain CNI networks

`
sudo sysctl net.bridge.bridge-nf-call-iptables=1
`

### Step 3: initialize kubeadm (done only for master)

`
kubeadm init --pod-network-cidr=10.244.0.0/16
`

### Step 4: create kubeconfig so the user can run kubectl commands

`
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
`

### Step 5: install flannel networking
`
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/v0.9.1/Documentation/kube-flannel.yml
`

### Step 6: Only when you want to use master node to host pods (since we have 1 node cluster)

`
kubectl taint nodes --all node-role.kubernetes.io/master-
`

# Test

`
kubectl get pods --all-namespaces
`
