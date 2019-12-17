# Sample steps for creating AWS EC2 instance via Ansible playbook
(1) Create AWS user via AWS IAM; save the "Access key ID" and "Secret access key"

(2) Install Ansible and the EC2 module dependencies
<br>$ pip3 install boto boto3 ansible

(3) Create SSH keys to connect to the EC2 instance (used after provisioning)
<br>$ ssh-keygen -t rsa -b 4096 -f ~/ansible/AWS/SSH/aws_access

(4) Create the Ansible directory structure
<br>$ mkdir -p group_vars/all

(5) Create Ansible Vault file to store the AWS Access and Secret keys
<br>$ ansible-vault create group_vars/all/ansible_vault_pass.yml

(6) Edit the ansible_vault_pass.yml file and create the keys global constants
<br>$ ansible-vault edit group_vars/all/ansible_vault_pass.yml

<br>— Include the variables ec2_access_key and ec2_secret_key in "ansible_vault_pass.yml" file
<br>—  ec2_access_key: xxxxxxxxxx
<br>—  ec2_secret_key: xxxxxxxxxx

(7) Create a EC2 provisioning playbook (ec2_playbook.yml)

(8) Run the playbook to provision a new EC2 instance
<br>$ ansible-playbook ec2_playbook.yml --ask-vault-pass --tags create_ec2

(9) Login to the newly created EC2
<br>$ ssh -i ~/ansible/AWS/SSH/aws_access ubuntu@"Filled in with EC2 public IP address or Public DNS"

** Note : If encountered the "IdempotentParameterMismatch." error, change “id” or “region” to some different values and run playbook again **
