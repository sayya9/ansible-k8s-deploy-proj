# ansible-k8s-deploy-proj
This ansible playbook will deploy company projects via helm of Kubernetes. OS platform can support CentOS 7 and Ubuntu 16.04.

INSTALL
=======

To clone:

```
git clone https://github.com/sayya9/ansible-k8s-deploy.git
cd ansible-k8s-deploy-proj
cp -a inventory/example inventory/your_server
```

To modify:

```
inventory/your_server/*
```

To deploy:

```
ansible-playbook -i inventory/your_server/inventory -b --ask-vault-pass install.yml
```

To delete projects:

```
ansible-playbook -i inventory/your_server/inventory -b delete.yml
```

Role Variables
=======
Available variables are listed below. (see inventory/example/group_vars/all.yml, example is your server name):

deploy_customer variable is your customer name. Kubernetes helm deploy projects in example namespace and load helm values.yaml files in roles/deploy/files/example.

```deploy_customer: example```


This is your helm repo URL

```
deploy_location: https://example/helm-repository
```

deploy_proj variable put your helm project list.

```
deploy_proj:
  - { chart: postgres, release: postgres, namespace: default, version: 10.3-alpine, enabled: True }
  - { chart: k8s-hostpath-provisioner, release: k8s-hostpath-provisioner, namespace: default, version: 0.1.0, enabled: True }
```

The directory [deploy/files/example](https://github.com/sayya9/ansible-k8s-deploy-proj/tree/master/roles/deploy/files/example) content put each helm project values.yml. Tips: example is your namespace(deploy_customer variable)

For example postgres:
```
global:
  image:
pullPolicy: IfNotPresent
```
