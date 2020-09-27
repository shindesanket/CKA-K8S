# Cluster Upgrade

---

[Upgrading from v1.15 to v1.16](https://v1-16.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

#### Upgrade the Control Plane Nodes

1. Deploy some workload on the cluster

```bash
kubectl run nginx-deploy --image=nginx:alpine --replicas=6
```

2. find the latest 1.16 version in the list

```bash
sudo su -
apt update
apt-cache policy kubeadm
```

3. Update kubeadm with the latest patch version
   
```bash
apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.16.14-00 && \
apt-mark hold kubeadm
```

4. Verify that the download works and has the expected version:

```bash
kubeadm version
# exit from root user
exit
```

5. Drain the control plane node:

```bash
kubectl drain kmaster --ignore-daemonsets
```

6. On the control plane node, run:

```bash
sudo kubeadm upgrade plan
```

7. Choose a version to upgrade to, and run the appropriate command. For example:

```bash
sudo kubeadm upgrade apply v1.16.14
```

8. Check the status of the node by using the command -

```bash
kubectl get nodes
```

9. Uncordon the control plane node

```bash
kubectl uncordon kmaster
```

10. Upgrade the kubelet and kubectl on all control plane nodes:

```bash
sudo apt-mark unhold kubelet kubectl && \
sudo apt-get update && sudo apt-get install -y kubelet=1.16.14-00 kubectl=1.16.14-00 && \
sudo apt-mark hold kubelet kubectl
```

11. Restart the kubelet

```bash
sudo systemctl restart kubelet
```

12. Check the version again using 

```bash
kubectl get nodes
```

#### Upgrade the kslave1 worker node

1. Prepare the node for maintenance by marking it `unschedulable` and `evicting the workloads`. 

```bash
# for demo purpose check the pods that are running on kslave1
kubectl get pods -o wide
kubectl drain kslave1 --ignore-daemonsets
# for demo purpose check the pods again after the drain command
kubectl get pods -o wide

```

2. SSH into the other worker node

```bash
ssh ubuntu@kslave1
```

3. Upgrade kubeadm on all worker nodes:

```bash
sudo apt-mark unhold kubeadm && \
sudo apt-get update && sudo apt-get install -y kubeadm=1.16.14-00 && \
sudo apt-mark hold kubeadm
```

4. Call the following command to upgrade the node:

```bash
sudo kubeadm upgrade node
```

5. Upgrade the kubelet and kubectl on all worker nodes:

```bash
sudo apt-mark unhold kubelet kubectl && \
sudo apt-get update && sudo apt-get install -y kubelet=1.16.14-00 kubectl=1.16.14-00 && \
sudo apt-mark hold kubelet kubectl
```

6. Restart the kubelet service

```bash
sudo systemctl restart kubelet
```

7. Exit from the kslave1 node

```bash
exit
```

8. Bring the node back online by marking it schedulable:

```bash
kubectl uncordon kslave1
```

9. Verify the status using

```bash
kubectl get nodes
```

10. Check the pods does not get added to kslave1 

```bash
kubectl get pods -o wide
```

Similarly,

#### Upgrade the kslave2 worker node

1. Prepare the node for maintenance by marking it `unschedulable` and `evicting the workloads`. 

```bash
# for demo purpose check the pods that are running on kslave1
kubectl get pods -o wide
kubectl drain kslave2 --ignore-daemonsets
# for demo purpose check the pods again after the drain command
kubectl get pods -o wide

```

2. SSH into the other worker node

```bash
ssh ubuntu@kslave2
```

3. Upgrade kubeadm on all worker nodes:

```bash
sudo apt-mark unhold kubeadm && \
sudo apt-get update && sudo apt-get install -y kubeadm=1.16.14-00 && \
sudo apt-mark hold kubeadm
```

4. Call the following command to upgrade the node:

```bash
sudo kubeadm upgrade node
```

5. Upgrade the kubelet and kubectl on all worker nodes:

```bash
sudo apt-mark unhold kubelet kubectl && \
sudo apt-get update && sudo apt-get install -y kubelet=1.16.14-00 kubectl=1.16.14-00 && \
sudo apt-mark hold kubelet kubectl
```

6. Restart the kubelet service

```bash
sudo systemctl restart kubelet
```

7. Exit from the kslave2 node

```bash
exit
```

8. Bring the node back online by marking it schedulable:

```bash
kubectl uncordon kslave2
```

9. Verify the status using

```bash
kubectl get nodes
```

10. Check the pods does not get added to kslave2

```bash
kubectl get pods -o wide
```

[Upgrading from v1.16 to v1.17](https://v1-17.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)


---

```bash
sudo su -
apt update
apt-cache madison kubeadm

# 1.17.11-00

# replace x in 1.17.x-00 with the latest patch version
apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.17.11-00 && \
apt-mark hold kubeadm

# since apt-get version 1.1 you can also use the following method
apt-get update && \
apt-get install -y --allow-change-held-packages kubeadm=1.17.11-00

kubeadm version

kubectl drain kmaster --ignore-daemonsets

sudo kubeadm upgrade plan

sudo kubeadm upgrade apply v1.17.11

kubectl uncordon kmaster


sudo su -

apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.17.11-00 kubectl=1.17.11-00 && \
apt-mark hold kubelet kubectl

# since apt-get version 1.1 you can also use the following method
apt-get update && \
apt-get install -y --allow-change-held-packages kubelet=1.17.11-00 kubectl=1.17.11-00

exit

sudo systemctl restart kubelet

kubectl drain kslave1

# replace x in 1.17.x-00 with the latest patch version
apt-mark unhold kubeadm && \
apt-get update && apt-get install -y kubeadm=1.17.11-00 && \
apt-mark hold kubeadm

# since apt-get version 1.1 you can also use the following method
apt-get update && \
apt-get install -y --allow-change-held-packages kubeadm=1.17.11-00

kubeadm upgrade node

# replace x in 1.17.x-00 with the latest patch version
apt-mark unhold kubelet kubectl && \
apt-get update && apt-get install -y kubelet=1.17.11-00 kubectl=1.17.11-00 && \
apt-mark hold kubelet kubectl

# since apt-get version 1.1 you can also use the following method
apt-get update && \
apt-get install -y --allow-change-held-packages kubelet=1.17.11-00 kubectl=1.17.11-00

systemctl restart kubelet

exit

exit

```


```bash
sudo docker image build -f Dockerfile1 -t <docker-id>/py-1:latest .
sudo docker image build -f Dockerfile2 -t <docker-id>/py-2:latest .

sudo docker container run --detach --rm --name python-app-1 --publish 8888:80 khozemanullwala/py-1:latest

sudo docker container exec -it python-app-1 bash


sudo docker container run -it --name alpine-demo --mount src=my-vol,dst=/xyz alpine sh


sudo docker container run -it --name alpine-two --mount src=my-vol,dst=/simplilearn alpine sh


sudo docker container run --name webserver --mount type=bind,src=$(pwd)/web-dir,dst=/usr/share/nginx/html,readonly --publish 10000:80 nginx:alpine
```
