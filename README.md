# ansible-k8s-deploy
This ansible playbook will deploy company projects via helm of Kubernetes. OS platform can support CentOS 7 and Ubuntu 16.04.

INSTALL
=======
```
git clone https://github.com/sayya9/ansible-k8s-deploy.git

cd ansible-k8s-deploy && ansible-playbook playbook.yml
```

Role Variables
=======
Available variables are listed below, along with default values (see deploy/defaults/main.yml):

This is your helm repo URL

```
deploy_location: https://example/helm-repository
```

Ansible playbook will load variable from deploy/vars/```example```.yml

```deploy_customer: example```

The file [deploy/vars/example.yml](https://github.com/sayya9/ansible-k8s-deploy/blob/master/roles/deploy/vars/example.yml) content put your helm project list.

```
deploy_proj:
  - { chart: postgres, release: postgres, namespace: default, version: 10.3-alpine, enabled: True }
  - { chart: k8s-hostpath-provisioner, release: k8s-hostpath-provisioner, namespace: default, version: 0.1.0, enabled: True }
```

The directory [deploy/files/example](https://github.com/sayya9/ansible-k8s-deploy-proj/tree/master/roles/deploy/files/example) content put each helm project values.yml.

For example postgres:
```
global:
  image:
pullPolicy: IfNotPresent
```
