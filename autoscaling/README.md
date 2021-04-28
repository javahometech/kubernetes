### Implementing auto scaling strategies in Kubernetes

## Install metrics server
### Prerequisites
you must allow service account tokens to communicate with kubelet, edit your cluster configuration
```console
$ kops edit cluster
```
add configuration below to your cluster configuration.
```
kubelet:
    anonymousAuth: false
    authorizationMode: Webhook
    authenticationTokenWebhook: true
```

update your cluster
```console
$ kops update cluster --yes
$ kops rolling-update cluster --yes
```
**Note:** Above command take a while based on your cluster size(For 3nodes it took 15mins)

In order to deploy metrics-server in your cluster run the following command

```console
# Kubernetes 1.8+ <= 1.15
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/kops/master/addons/metrics-server/v1.8.x.yaml

# Kubernetes 1.16+
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/kops/master/addons/metrics-server/v1.16.x.yaml
```
#### To check metric-server status
```
$ kubectl get pods --namespace kube-system | grep metrics-server
``` 
## HPA Setup
#### To create deployment run the below command
```
$ kubectl apply -f hpa.yml
```
#### To create horzontal pod autoscaler run below command
```
$ kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10
```
#### To check the status of horzontal pod autoscaler run below command
```
$ kubectl get hpa
```
#### To increase load on above deployment run below command
```
kubectl run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache; done"
```
For more details [Click here](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/)
