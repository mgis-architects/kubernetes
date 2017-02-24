# Pre-Requesites

## Install Ansible

**Add the EPEL Repository**

rpm -iUvh http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-9.noarch.rpm

**Install Ansible rpm**

```
yum -y install ansible
```

**Install libs**

```
yum -y install python-netaddr
```

**Install PIP**

```
yum -y install python-pip gcc python-devel python-lxml openssl-devel
pip install --upgrade pip
pip install "azure==2.0.0rc5"
pip install "msrestazure"
```
## Generate RSA keypair

Use your favorite tool to generate RSA keypair for the host authentication

# Install k8s cluster

## Step #1: Provision the infrastructure

Use terraform to build infrastructure required for k8s run. 
While doing so you will have to generate SSL key which will
subsequently be used with Ansible.

[Terraform for k8s](https://github.com/mgis-architects/terraform/tree/master/azure/k8s.form)

## Step #2: Execute Ansible build

Unfortunately due to Ansible bug delegate_to directive is not handled
correctly for dynamic inventory and we have to use static one.

Update ansible/invenvory/hosts file with the Terradorm build infra.

Execute the cluster build:

```
cd ansible/scripts/ && ./deploy-cluster.sh --private-key ~/.ssh/azu_priv.ppk
```