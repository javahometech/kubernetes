# Kubernetes Pods - Commands 
## Creating a Pod
### Create pod.yml with following content [pod.yml](https://github.com/javahometech/kubernetes/pods/pod.yml)
```
apiVersion: v1
kind: Pod
metadata:
  name: nodeapp
spec:
  containers:
  - name: nodeapp
    image: kammana/node-app:0.0.3
```

```
$ kubectl create -f pods.yml
```
### Command to get all pods

```
$ kubectl get pods
```

### Command to describe pod details

```
$ kubectl describe pods/nodeapp
```
Note: Replace nodeapp with your pod name
