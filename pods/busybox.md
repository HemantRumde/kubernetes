# busybox pod
busybox is a tiny collection of Unix/Linux utilities. It is useful for debug and trouble-shooting issues in k8s cluster. 
> busybox.yml 
```
kind: Pod
apiVersion: v1
metadata:
  annotations:
    author: Hemant Rumde
  name: busybox-pod
  namespace: mypods
  labels:
    application: busybox-pod-demo-01
spec:
  containers:
   - name: busybox01
     image: busybox:1.29
     command:
       - "sleep"
       - "30000"
```
# PyCharm IDE
PyCharm is a Python IDE. However it provides plugins for K8S yaml definitions. This saves lots of time to craft API resources.
> Download PyCharm Community version 
* Refer following URL of Kubernetes and OpenShift document
```
https://plugins.jetbrains.com/plugin/9354-kubernetes-and-openshift-resource-support
```
# Creating a pod
* Create a new pod
```kubectl create -f busybox.yml```
* List pods with short description ( name in metadata defines a name of pod )
```
kubectl get pods
kubectl get pod/busybox-pod
```
* Details description. Check all the events at the bottom of full description 
```
kubectl describe pod/busy-pod 
```
* Select pod by its label 
```
kubectl get pod -l application=foo-pod-demo-02
```
* A command used to create a pod can be recorded into annotations by <code>--record</code> option 
```
kubectl create -f busybox.yml --record
```
