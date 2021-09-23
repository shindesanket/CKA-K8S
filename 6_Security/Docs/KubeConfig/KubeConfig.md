# Explore Kubeconfig file

## Kubeconfig File
- The kubeconfig file has 3 sections
  - Clusters
  - Contexts
  - USers

- To view the current file being used
  ```
  $ kubectl config view
  ```
- You can specify the kubeconfig file with kubectl config view with "--kubeconfig" flag
  ```
  $ kubectl config view --kubeconfig=my-custom-config

- How do you update your current context? Or change the current context
  ```
  $ kubectl config view --kubeconfig=my-custom-config
  ```
  - kubectl config help
  ```
  $ kubeclt config -h
  ```
## Practice

- Run the kubectl config view command and count the number of clusters

    
- Run the command 'kubectl config view' and count the number of users
  
- How many contexts are defined in the default kubeconfig file?
  
  
- Run the command 'kubectl config view' and look for the user name.
  
  
- What is the name of the cluster configured in the default kubeconfig file?

#### K8s Reference Docs
- https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/
- https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#config
