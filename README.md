# Pre-Requesites

## Install Ansible

### Step #1: Add the EPEL Repository

rpm -iUvh http://dl.fedoraproject.org/pub/epel/7/x86_64/e/epel-release-7-9.noarch.rpm

### Step #2: The Installation

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
### Step #3: Provision the infrastructure

Use terraform to build infrastructure required for k8s run. 
While doing so you will have to generate SSL key which will
subsequently be used with Ansible.

### Step #4: Execute Ansible build

Unfortunately due to Ansible bug delegate_to directive is not handled
correctly for dynamic inventory and we have to use static one.

Update ansible/invenvory/hosts file with the Terradorm build infra.

Execute the cluster build:

```
cd ansible/scripts/ && ./deploy-cluster.sh --private-key ~/.ssh/azu_priv.ppk
```