



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

After running the command below you should recieve a succes message 

"Your Kubernetes master has initialized successfully!"

You will also see code with the format below

"sudo kubeadm join --token <token> <IP>:6443 --discovery-token-ca-cert-hash
<hash>"

Copy this code you will need it later to add worker nodes to the cluster.

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

### Step 6: Only when you want to use master node to host pods 

`
kubectl taint nodes --all node-role.kubernetes.io/master-
`

### Test

`
kubectl get pods --all-namespaces

## Worker Nodes

### Step 1: Sign in as Root

sudo su

### Step 2: pass bridged IPv4 traffic to iptables` chains which is required by certain CNI networks

`
sudo sysctl net.bridge.bridge-nf-call-iptables=1
`

### Step 3: Get the token that you copied from step 3 above and run in the new node

"sudo kubeadm join --token <token> <IP>:6443 --discovery-token-ca-cert-hash
<hash>"

If you don't have the informaiton you can run the follwoing code on the master

`
kubeadm  token create --print-join-command
`

### Test:  Return to master node and run the below command to see if worker nodes have joined cluster 

`
kubectl get nodes
`


 

