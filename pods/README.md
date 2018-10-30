# Kubernetes Pods - Commands 
## Creating a Pod
### Create pod.yml with following content
Get the file [here(pod.xml)](https://github.com/javahometech/kubernetes/pods/pod.yml)
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
**Syntax - kubectl describe pods/POD_NAME**

```
$ kubectl describe pods/nodeapp
```

### Executing commands on pods
**Syntax - kubectl exec POD_NAME CMD_TO_EXECUTE**
```
$ kubectl exec nodeapp printenv
```


