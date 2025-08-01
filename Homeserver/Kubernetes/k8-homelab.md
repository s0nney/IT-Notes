So you fell into the container orchestration world. Look no further than using Kubernetes to spin up a cluster of your
own!

## Setup

Prerequisites: 
- A single dedicated computer running proxmox 
- Preferably the latest Ubuntu server version
- Coffee

VMs:
- 1 Controller VM 
- 1 or more Node VMs 
- Disable swap memory on ALL vms.


Update, download the base packages for our cluster setup, then reboot.
- sudo apt update && sudo apt upgrade -y && sudo apt install docker.io docker-compose curl gnupg containerd wget apt-transport-https ca-certificates qemu-guest-agent && sudo reboot


## Installing kubeadm, kubectl, and kubelet

We're going to be using Ubuntu's native package management because snap is a mess.

```
sudo mkdir -p -m 755 /etc/apt/keyrings

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.33/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

sudo chmod 644 /etc/apt/keyrings/kubernetes-apt-keyring.gpg 

echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.33/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo chmod 644 /etc/apt/sources.list.d/kubernetes.list   
```

Edit in order: 
- /etc/containerd/config.toml
- /etc/fstab (check if swap is enabled: free -m)
- /etc/sysctl.conf
- /etc/modules-load.d/k8s.conf

Reboot.
