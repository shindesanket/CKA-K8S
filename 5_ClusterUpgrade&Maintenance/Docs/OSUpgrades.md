# Drain UnCordon and Cordon

## List the nodes to identify node for maintenance

```bash
kubectl get nodes
```

## Check the status of pods. On which nodes pods are scheduled

```bash
kubectl get pods -o wide
```

## To evict the pods and mark node unschedulable

```bash
kubectl drain <node name> --ignore-daemonsets
```

## Observe that pods are evicted and scheduled on other node

```bash
kubectl get pods -o wide
```

## Observe that node has been marked as SchedulingDisabled

```bash
kubectl get pods -o wide
```

## Uncordon the node now and check if again old pods are scheduled on it or not

```bash
kubectl uncordon <node name>
```

## Old Pods are not scheduled. So lets create new pods now and check

```bash
kubectl create deployment nginx-demo --image nginx
kubectl scale deployment nginx-demo --replicas 6
```

## To just mark nodes unschedulable

```bash
kubectl cordon <node name>
```

## Create new deployment and observe that cordoned node is not used while scheduling

```bash
kubectl create deployment nginx-demo123 --image nginx
kubectl scale deployment nginx-demo123 --replicas 6
```
