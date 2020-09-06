# Setting up Self Managed Cluster on local machine using kubeadm and on cloud

1. Install Container Runtime (Docker) on all the nodes

```bash
sudo apt update
sudo apt install -y docker.io
sudo systemctl enable docker.service
```

2. Install Kubernetes on all the nodes

```bash
sudo apt install -y apt-transport-https curl

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -

cat <<EOF | sudo tee /etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF

sudo apt-get update

sudo apt-get install -y kubelet kubeadm kubectl

sudo apt-mark hold kubelet kubeadm kubectl
```

3. On the controller VM, execute:

```bash
sudo kubeadm init --pod-network-cidr 192.168.0.0/16
```

4. On the controller VM, to set up kubectl for the ubuntu user, run:

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

5. On the other nodes execute the `kubeadm join` command, found at the end of the output of `kubeadm init` command.

6. On the controller, verify that all nodes have joined

```bash
kubectl get nodes
```

7. On the controller, install Calico from the manifest:

```bash
curl https://docs.projectcalico.org/manifests/calico.yaml -O
kubectl apply -f calico.yaml
```

8. On the controller, verify that all nodes are ready

```bash
kubectl get nodes
```