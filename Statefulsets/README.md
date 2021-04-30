# Statefulsets

**Note:** This tutorial assumes that your cluster is configured to dynamically provision PersistentVolumes. If your cluster is not configured to do so, you will have to manually provision two 1 GiB volumes prior to starting this tutorial.

#### To create statefusets run the below command
```
$ kubectl apply -f statefulset.yaml
```
#### To check the created service run below command
```
$ kubectl get service nginx
```
#### To check created statefulset run below command
```
$ kubectl get statefulset web
```
