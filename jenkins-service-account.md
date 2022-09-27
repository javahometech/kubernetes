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
pipeline{
    agent any
    stages{
        stage("Welcome"){
            steps{
                echo "Welcome to Pipelines"
                withCredentials([kubeconfigFile(credentialsId: 'k8s-creds', variable: 'KUBECONFIG')]) {
                    sh "echo $KUBECONFIG "
                }
            }
        }
    }
}
