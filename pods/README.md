# Kubernetes Pods - Commands 
## Creating a Pod
### Create pod.yml with following content
Get the file [(pod.yml)](https://github.com/javahometech/kubernetes/blob/master/pods/pods.yml)
```
apiVersion: v1
kind: Pod
metadata:
  name: nodeapp
  labels:
    app: nodeapp
spec:
  containers:
    - name: nodeapp
      image: kammana/nodeapp:v1
      ports:
        - containerPort: 8080
```

```
$ kubectl create -f https://raw.githubusercontent.com/javahometech/kubernetes/master/pods/pods.yml
```
### Command to get all pods

```
$ kubectl get pods
```

### Command to describe pod details
**Syntax** - kubectl describe pods/POD_NAME

```
$ kubectl describe pods/nodeapp
```

### Executing commands on pods
**Syntax** - kubectl exec POD_NAME CMD_TO_EXECUTE
```
$ kubectl exec nodeapp printenv
```
### Getting into pods Terminal
**Syntax** - kubectl exec -it POD_NAME bash
```
$ kubectl exec -it nodeapp bash
```
### Get logs from pods
**Syntax** - kubectl logs POD_NAME
```
$ kubectl logs nodeapp
```
## Exposing Pods to Internet
By default Pods run in a isolated environment i.e. they are reachable within kubernetes cluster, if you wanna reach your pod outside cluster, You have to expose it
```
$ kubectl expose pods/nodeapp --type="NodePort" --port 8080
```


