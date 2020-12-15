## Deployments
It is a kubernetes object which the declarative updates for Pods and ReplicaSets

### Create Deployment 

```
kubectl create -f https://raw.githubusercontent.com/javahometech/kubernetes/master/deployments/deployments.yml --record=true
```

### Check status of the current deployment

```
kubectl rollout status deployment nodeapp
```

### Updating deployment
For example we want to change number of replicas, change replicas in yaml and run following command

```
kubectl apply -f https://raw.githubusercontent.com/javahometech/kubernetes/master/deployments/deployments.yml  --record=true
```

### Kubernetes Deployment revisions
Kubernetes maintains deployment state of all versions

inorder to see deployment revision history

```
kubectl rollout history deployment nodeapp
```

### Undo recent deployment

```
kubectl rollout undo deployment nodeapp
```

### rollback to specific deployment revision 

```
kubectl rollout undo deployment nodeapp --to-revision=1
```
