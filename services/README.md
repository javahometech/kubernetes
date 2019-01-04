# Kubernetes Service Objects
- In kubernetes service is an object that is logically mapped to pods based on labels.
- Service can be single point of contact like loadbalancer for set of pods.
- By default Pod is not expose to the internet or outside of the cluster, by using service Pod is exposed to internet.
- Any Pod create in future is added to service dynamicaly if pod label is matching with Service lable selector.  

![service](https://github.com/javahometech/kubernetes/blob/master/images/service.png)
