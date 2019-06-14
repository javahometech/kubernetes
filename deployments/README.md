## Deployments
It is a kubernetes object which the declarative updates for Pods and ReplicaSets

### Create Deployment 

```
kubectl create -f https://raw.githubusercontent.com/javahometech/kubernetes/master/deployments/deployments.yml
```

### Check status of the current deployment

```
kubectl rollout status deployment nodeappdeployment
```

### Updating deployment
For example we want to change number of replicas, change replicas in yaml and run following command

```
kubectl apply -f https://raw.githubusercontent.com/javahometech/kubernetes/master/deployments/deployments.yml
```
