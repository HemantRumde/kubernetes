# How to use your private docker repository?

This method is not safe for production. However it would explain relationship between ServiceAccount, Secret and Pod.
I am using Pod for simplicity. You can use this in Deployments.

> Your Docker Hub credentials

Attribute     | Value
------------- |---------------
login         | hemant
password      | ******

---
## Step 01: Create a Secret
```
  kubectl create secret docker-registry docker_access \
  --docker-username=hemant \
  --docker-password=****** \
  --docker-email=hemant@unicom.com

```
Above command would create a secret <code>docker-registry</code>. A service account would specify this secret.
We have not create a ServiceAccount for this. Let us create a new ServiceAccount

---
## Step 02: Create a ServiceAccount <code>hemant</code>
```
  kubectl create serviceaccount hemant
  kubectl get secrets
```
---
## Step 03: Associate ServiceAccount with Secret
```
  kubectl patch serviceaccount hemant \
  -p "{\"imagePullSecrets\": [{\"name\": \"docker-registry\"}]}"
```
---
## Step 04: In Pod yaml file use ServiceAccount
```
    kind: Pod
    apiVersion: v1
    metadata:
      annotations:
        author: Hemant Rumde
      name: foo-pod
      namespace: development
      labels:
        application: foo-pod-demo-01
    spec:
      serviceAccount: hemant
      containers:
       - name: mysh
         image: hemantrumde/mysh:1.1
         command:
            - "sleep"
            - "30000"
```
