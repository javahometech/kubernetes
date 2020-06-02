## 1. Pulling private images using Secrets

#### Create kubernetes secrets using command line

```
kubectl create secret docker-registry regcred --docker-server=https://index.docker.io/v1/ --docker-username=kammana --docker-password=<your-password> --docker-email=hari.kammana@gmail.com
```
#### Create ssecrets using config.json

The following command will create config.json file in your <home-dir>/.docker/config.json
```
docker login
```

```
kubectl create secret generic regcred --from-file=.dockerconfigjson=/home/ec2-user/.docker/config.json --type=kubernetes.io/dockerconfigjson
```

After create secret, lets create pod which uses private images.

```
apiVersion: v1
kind: Pod
metadata:
  name: private-reg
spec:
  containers:
  - name: privateapp
    image: kammana/privateapp:0.0.1
  imagePullSecrets:
  - name: regcred

```

Create pod which uses private image 

```
kubectl create -f https://raw.githubusercontent.com/javahometech/kubernetes/master/secrets/private-images-pod.yml
```
