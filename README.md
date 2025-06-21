# Kubernetes node setup with ansible

This repo contains the playbooks used to setup Kubernetes nodes Master (control plane) and workers on Ubuntu vm

## What is being done

I **highly recommend** reading through both the playbooks to fully understand what is being done. 

The general of what is happening
1. Update apt package index
2. Install required system packages
3. Load kernel modules for containerd
4. Set sysctl parameters for Kubernetes networking
5. Add Docker GPG key and repository
6. Install containerd and configure SystemdCgroup
7. Add Kubernetes GPG key and repository (v1.33)
8. Install kubelet, kubeadm, and kubectl
9. Disable swap and clean up fstab
10. Start and enable kubelet and containerd

## requirements
- ssh access to the hosts targets

## Usage
1. Access repository 
Clone repo
cd into repo

2. edit inventory.ini ( I am using yaml inventory formatting because I personally prefer it)
```yaml
all:
  hosts:
    Master-node:
      ansible_host: 192.168.1.3
    worker1:
      ansible_host: 192.168.1.4
    worker2:
      ansible_host: 192.168.1.5
```
4. Run Python install playbook ( optional. on a fresh VM I had to install it so I decided to add it just in case)

ansible-playbook -i inventory.ini install-py.yml -u USER --become --ask-become-pass

6. Run Kubernetes install playbook

ansible-playbook -i inventory.ini install-kube.yml -u USER --become --ask-become-pass

## Post install

This is where you can log on the the Master and works and start initalising the cluster
