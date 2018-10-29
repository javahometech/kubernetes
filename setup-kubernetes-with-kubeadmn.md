# Under construction

# Configure Kubernetes With Kubeadm

## I'll be demonstrating with three CentOS 7 servers (at the following IP addresses)
```
192.168.33.10 Master
192.168.33.11 worker1
192.168.33.12 worker2
```
### In case you don’t have your own dns server then update /etc/hosts file on master and worker nodes
```
192.168.33.10 Master
192.168.33.11 worker1
192.168.33.12 worker2
```
### Before you start setting up Kubernetes cluster, it is recommended that you update your system to ensure all security updates are up-to-date
```sh
$sudo yum update -y
```
## `Note`: 
### Ensure swap is disabled on both master and worker nodes. Kubernetes requires swap to be disabled in order for it to successfully configure Kubernetes Cluster
### command to disable swap
```sh
$sudo swapoff -a
```
### check swap is disabled
```sh
$cat /proc/swaps
```
### command to update fstab so that swap remains disabled after a reboot
```sh
$sudo sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
```
### In order for Kubernetes cluster to communicate internally, we have to disable `SELinux`
### Disable SELinux
```sh
$sudo setenforce 0
```
###To check SELinux:
```sh
$ sestatus
```
### If SELinux still enabled run add SELINUX=disabled to below file and comment SELINUX=enforcing
```sh
$sed -i --follow-symlinks 's/SELINUX=enforcing/SELINUX=disabled/g' /etc/sysconfig/selinux
```
