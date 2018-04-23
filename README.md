# ansible-k8s-deploy-proj
This ansible playbook will deploy company projects via helm of Kubernetes. OS platform can support CentOS 7 and Ubuntu 16.04.

INSTALL
=======

Clone this repo:

```
git clone https://github.com/sayya9/ansible-k8s-deploy.git
cd ansible-k8s-deploy-proj
cp -a inventory/example inventory/your_server
```

To modify:

```
inventory/your_server/*
```

### For external network environment installation

Install pygit2

```
ansible-playbook -i inventory/your_server/inventory -b pygit2.yml
```

Deploy projects:

```
ansible-playbook -i inventory/your_server/inventory -b --ask-vault-pass deploy.yml
```

Upgrade projects:

```
ansible-playbook -i inventory/your_server/inventory -b upgrade.yml
```

### For internal network environment installation

Prepare images:

Don't forget to put ~/.kube/config and  ~/.docker/config.json

```
ansible-playbook -i inventory/your_server/inventory prepare.yml
```

Copy to customer server:

```
scp -r . remote_server:~/ansible-k8s-deploy-proj
```

Delete projects:

```
ansible-playbook -i inventory/your_server/inventory -b delete.yml
```

Role Variables
=======
Available variables are listed below. (see inventory/example/group_vars/all.yml, example is your server name):

chart_repo_name variable is helm chart repo name, it is used by the command blew.

chart_repo_name variable

```
chart_repo_name: example
```

command

```
helm repo add example https://example/helm-repository
```

customer variable is your customer name. Kubernetes helm deploy projects in example namespace and load helm values.yaml files in roles/deploy/files/example.

```customer: example```


This is your helm repo URL

```
location: https://example/helm-repository
```

projects variable put your helm project list.

```
projects:
  - { chart: postgres, release: postgres, namespace: default, version: 10.3-alpine, enabled: True }
  - { chart: k8s-hostpath-provisioner, release: k8s-hostpath-provisioner, namespace: default, version: 0.1.0, enabled: True }
```

The directory [roles/deploy/files/example](https://github.com/sayya9/ansible-k8s-deploy-proj/tree/master/roles/deploy/files/example) content put each helm project values.yml. Tips: example is your namespace(customer variable). In other words, Kubernetes will create the name example namespace.

For example postgres:
```
global:
  image:
pullPolicy: IfNotPresent
```
