### Implementing auto scaling strategies in Kubernetes

## Install metrics server

```
   git clone https://github.com/kubernetes-incubator/metrics-server.git
```

```
   kubectl run php-apache --image=k8s.gcr.io/hpa-example --requests=cpu=200m --expose --port=80
```
