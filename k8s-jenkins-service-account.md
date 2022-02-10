## Steps to configure kubernetes service account for Jenkins

```
  kubectl -n kube-system create serviceaccount jenkins-sa
  
  kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:jenkins-sa

  TOKENNAME=`kubectl -n kube-system get serviceaccount/jenkins-sa -o jsonpath='{.secrets[0].name}'`

  TOKEN=`kubectl -n kube-system get secret $TOKENNAME -o jsonpath='{.data.token}'| base64 --decode`

  kubectl config set-credentials jenkins-sa --token=$TOKEN
```

## Jenkins Code Snippet

```
withCredentials([kubeconfigFile(credentialsId: 'kubeconfig', variable: 'KUBECONFIG')]) {
                    sh "/usr/local/bin/kubectl apply -f kubernetes/pod.yml  "
                }
```
