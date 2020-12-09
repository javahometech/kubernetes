# Configure Kubernetes Cluster With Kubeadm

## 1. Take 3 Linux servers (I'Ve taken AWS Linux 3 servers)
```
  One node for master and other two workers
```

## 2. Repeate these steps on all three nodes

  * ### Install docker on all nodes
  ```
      sudo yum install docker -y
      sudo service docker start
      sudo chkconfig docker on
  ```
  
  * ### Adding current user to docker group (Optional)
      ```
        sudo usermod -aG docker $USER
        sudo service docker start 
      ```
  * ### Disable swap momory
  
      ``` 
        sudo swapoff -a 
      ```
    
  * ### Command to update fstab so that swap remains disabled after a reboot
  
      ``` 
        sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab 
      ```
    
  * ### Set SELinux in permissive mode (effectively disabling it)
  
  ```
        sudo setenforce 0
        sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
  ```
  
  * ### Install kubeadmn, kubectl, kubectl on all three nodes
      
```
cat <<EOF | sudo tee /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-\$basearch
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
exclude=kubelet kubeadm kubectl
EOF
```
```
sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
sudo systemctl enable --now kubelet
```     
## 3. Initialize kubernets cluster on Master node(Run this only on master)
    sudo kubeadm init
        
## 4. Do following setup to start using kubernetes cluster(Run this only on master)
  ```
    mkdir -p $HOME/.kube
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
  ```
## 5. Add pod network add-ons (Run this only on master)
  
    kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
        
  ## 6. Take note of kubeadm command and run on all workers
  
  ```
    Run this command(replace with your command) on every node to join the cluster
  
    sudo kubeadm join 172.31.44.226:6443 --token f6o4a3.jdagdd4e2h8xhzy1 \
      --discovery-token-ca-cert-hash sha256:d0528baca6a2cf15bfece995d7df6f5d018b233b54251716ce2fd984148ba6d6
 ```
 
  ## 7. Get list of nodes in the cluster (Run this on master)
  
  ```
  kubectly get nodes
 ```
 

        
