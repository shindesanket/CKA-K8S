# Certificates API

## CA (Certificate Authority)
- The CA is really just the pair of key and certificate files that we have generated, whoever gains access to these pair of files can sign any certificate for the kubernetes environment.

#### Kubernetes has a built-in certificates API that can do this for you. 
- With the certificate API, we now send a certificate signing request (CSR) directly to kubernetes through an API call.

#### This certificate can then be extracted and shared with the user.
- A user first creates a key
  ```
  $ openssl genrsa -out jane.key 2048
  ```
- Generates a CSR
  ```
  $ openssl req -new -key jane.key -subj "/CN=jane" -out jane.csr 
  ```
- Sends the request to the administrator and the adminsitrator takes the key and creates a CSR object, with kind as "CertificateSigningRequest" and a encoded "jane.csr"
  
```yml
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: jane
spec:
  request: <<< CSR in base 64 format >>>
  signerName: kubernetes.io/kube-apiserver-client
  usages:
  - client auth
 ```
  
  ```bash
  cat jane.csr | base64 | tr -d "\n"
  kubectl apply -f jane.yaml
  ```
  
- To list the csr's
  ```bash
  kubectl get csr
  ```
- Approve the request
  ```bash
  $ kubectl certificate approve jane
  ```
- To view the certificate
  ```bash
  $ kubectl get csr jane -o yaml
  ```
- To decode it
  ```bash
  $ echo "<certificate>" | base64 --decode
  ```

---
