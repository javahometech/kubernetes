## 1. Install Helm Package Manager

  ```
  wget https://get.helm.sh/helm-v3.3.1-linux-amd64.tar.gz
  tar -zxvf helm-v3.3.1-linux-amd64.tar.gz
  mv linux-amd64/helm /usr/local/bin/helm
  ```
  
## 2. Install Helm Package Manager
  ```
  kubectl create ns monitoring
  
  helm install stable/prometheus-operator
  ```
