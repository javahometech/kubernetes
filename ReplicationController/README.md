## ReplicationController
- A ReplicationController ensures that a desired number of pod replicas are running at any one time.
- A ReplicationController makes sure that a pod or a homogeneous set of pods is always up and available

### Working style of ReplicationController
- ReplicationController creates if less number of pods are available or terminates extra pods if there are too many pods
- It replaces if any one of pod is deleted or failed.
- ReplicationController supervises multiple pods across multiple nodes
- ReplicationController is often abbreviated to **"rc"** or **"rcs"** in discussion, and as a shortcut in kubectl commands.

**EX:-** If pods are re-created on a node after disruptive maintenance such as a kernel upgrade. for this reason, use ReplicationController if if your application require only single-pod

![ReplicationController](https://github.com/javahometech/kubernetes/blob/master/images/ReplicationController.png "ReplicationController")

## Creating a ReplicationController
### Create rc.yml with following content
Get the file [(rc.yml)](https://github.com/javahometech/kubernetes/blob/master/ReplicationController/rc.yml)
```
apiVersion: v1
kind: ReplicationController
metadata:
  name: nodeapp
spec:
  replicas: 3
  selector:
    app: nodeapp
  template:
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

### Command to create ReplicationController
**Syntax:** kubectl create -f FILE_NAME
```
$ kubectl create -f rc.yml
```
###  Command to get all ReplicationController
**Syntax:** kubectl get rc
```
$ kubectl get rc
```
### Command to describe ReplicationController
**Syntax:** kubectl describe rc REPLICATIONCONTROLLER_NAME
```
$ kubectl describe rc nodeapp
```
### Command to Expose ReplicationController to Internet
By default ReplicationController run in a isolated environment i.e. they are reachable within kubernetes cluster, if you wanna reach your ReplicationController outside cluster, You have to expose it

**Syntax:** kubectl expose rc REPLICATIONCONTROLLER_NAME --type="NodePort" --port CONTAINER_PORT
```
$ kubectl expose rc nodeapp --type="NodePort" --port 8080
```
