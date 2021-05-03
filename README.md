# k3s Raspberry Pi Home Project
The project will be installing Kubernetes cluster on Raspberry Pi 4's 64 bit:
- Ubuntu Server 20.04.2 LTS
- arm64 processor

# Prerequisites for System Requirements
- Deploy Ansible 2.4.0+ to your local environment
- Make sure your Raspberry Pi's are accessible via passwordless SSH access.
- To find your ip address use `ip a` in Linux or `ifconfig` on macOS.
  - use `nmap -sn <ip_address_here>` (ex. `nmap -sn 10.0.100.1/24`)

# Usage
To begin this project, I have created a folder which will contain the necessary requirements to run our build:
Refer to directory `inventory/k3s-cluster/hosts.ini` to match your Raspberry Pi's IP addresses to your liking. Here is an example that is provided:

```
[master]
192.16.35.12

[node]
192.16.35.[10:11]

[k3s_cluster:children]
master
node
```

In `inventory/k3s-cluster/groups_vars/all.yml`, match your environment to what has been installed.

Finally, being provisioning your cluster using the following command:
`ansible-playbook site.yml -i inventory/k3s-cluster/hosts.ini`

# Kubeconfig
To get access to your Kubernetes cluster, use this command:
`scp debian@master_ip:~/.kube/config ~/.kube/config`

# Acknowledgements
This project could not be achieved without the help of Rancher's k3s-ansible repo. Please refer to repo [k3s-ansible](https://github.com/k3s-io/k3s-ansible) which uses Ansible to install k3s on Raspberry's ARM chips. This repo is extremely helpful. Note: I would recommend using k3s on Raspberry Pi's since k8s is power hungry when it comes to resources. Best to stick with k3s.