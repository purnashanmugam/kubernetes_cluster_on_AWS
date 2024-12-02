Deploying a Kubernetes cluster can be a complex task, but using Ansible to automate the process can simplify it significantly. This article will guide you through deploying a Kubernetes cluster on Ubuntu 24.04 machines provisioned on AWS EC2 instances. We will cover the prerequisites and step-by-step instructions to achieve this deployment.
Use Case:
  Create Ansible Playbook to launch 3 AWS EC2 Instance
  Create Ansible Playbook to configure Docker over those instances
  Create Playbook to configure K8S Master, K8S Worker Nodes on the above created EC2 Instances using kubeadm


Pre-requisites:
1) Controller node should be installed with python 3.12.3, pip 24.0, ansible 11.0.0
```
sudo apt update
sudo apt install python3
sudo apt install python3-pip
pip install ansible
```
2) Create one IAM user having Administrator Access and note down their access key and secret key
3) Create one Key pair in (.pem) format on AWS Cloud, download it in your local
4)Create a password for vault.
```
openssl rand -base64 2048 > vault_k8s.pass
ansible-vault create group_vars/all/pass.yml --vault-password-file vault_k8s.pass
```
5) Add your AWS credentials in pass.yml
```
access_key: #######
secret_key: #######
```
Run your Ansible Playbook
```
ansible-playbook setup.yml --vault-password-file vault_k8s.pass
```
