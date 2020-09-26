
# Project Discussion

## Autoscaling

Cluster Autoscaler - Adds the nodes dyanmically based on your pod status. Many pods are in pending state due to resource limitation.
Horizontal Pod Autoscaler - Deals with pods. Adds new pods when memory or cpu is about to exhaust.

[Autoscaling in Azure](https://docs.microsoft.com/en-us/azure/aks/cluster-autoscaler)
[Autoscaling in GCP](https://kubernetes.io/blog/2016/07/autoscaling-in-kubernetes/)

## Best Practices for production kubernetes cluster

1). RBAC - Decide identity management solution. Role, RoleBindings, ClusterRole, ClusterBindings

2). Ingress Controllers - Add your self signed certificates and host as https. add atleast 4-5 different ingress routes. [Link for ingress TLS](https://kubernetes.io/docs/concepts/services-networking/ingress/#tls)

3). Create atleast 3 namespaces. Dev, UAT, Prod. Attach resource quotas for namespaces.

4). Try to implement Daemonsets, node affinity, add taint for one node. (Pod Affinity, Pod Anti Affinity)
( 5 nodes, 3 pods, each pod should be deployed on separate nodes)

5). Add Cronjobs for small DB activities. [cron jobs]("https://kubernetes.io/docs/concepts/workloads/controllers/cron-jobs/")

6). Implement Liveliness and Readiness probes. ("https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-readiness-probes")

7). Try to add strong monitoring solution. (Prometheus, Azure monitor, AWS Cloudwatch)

8). Learn about Helm ( Package Manager for Kubernetes ). Deploy resources using Helm Chart.

9). Implement CI/CD Setup.

10). Velero (Velero.io) - Backup management system.

CKA Imp Links :

1). https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#logs
2). https://kubernetes.io/docs/reference/kubectl/cheatsheet/
3). https://kubernetes.io/docs/home/