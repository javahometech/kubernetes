### Create secrets.yml with following content
Get the file [(secrets.yml)](https://github.com/javahometech/kubernetes/blob/master/serviceaccount/secrets.yaml)
```
apiVersion: v1
kind: Secret
metadata:
   name: default-token-abcd  
   namespace: default
   annotations:
     kubernetes.io/service-account.name: jenkins
     kubernetes.io/service-account.namespace: default
type: kubernetes.io/service-account-token
```
```
$ kubectl create -f https://raw.githubusercontent.com/javahometech/kubernetes/master/serviceaccount/secrets.yaml
```

### Command to get all secrets

```
$ kubectl get secrets
```
### Create sa.yml with following content
Get the file [(sa.yml)](https://github.com/javahometech/kubernetes/blob/master/serviceaccount/sa.yaml)
```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: jenkins
  namespace: default
secrets:
- name: default-token-abcd
```
```
$ kubectl create -f https://raw.githubusercontent.com/javahometech/kubernetes/master/serviceaccount/sa.yaml
```
### Command to get all service accounts

```
$ kubectl get sa
```
### Create cluster role binding with following command.
```
kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=default:jenkins
```

### Get token name, where the token stored.
```
TOKENNAME=`kubectl  get serviceaccount/jenkins -o jsonpath='{.secrets[0].name}'`
```

### Get token, which is stored in the secret.
```
TOKEN=`kubectl get secret $TOKENNAME -o jsonpath='{.data.token}'| base64 --decode`
```

### Set the credentials to jenkins
```
kubectl config set-credentials jenkins --token=$TOKEN
```


### Set the context to jenkins user.
```
kubectl config set-context --current --user=jenkins
```
