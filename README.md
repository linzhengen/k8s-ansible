# k8s-ansible
### Prerequisite

- Vagrant(1.7.0+)
- VirtualBox(12.0.7+)

## 環境構築手順

- vagrantからマシンを起動する
```bash
$ cd k8s-ansible
$ vagrant up 
```

- master1にansibleをインストール
```bash
[vagrant@master1 ~]$ vagrant ssh master1
[vagrant@master1 ~]$ sudo yum install ansible -y
[vagrant@master1 ~]$ ansible --version
ansible 2.4.1.0

# 初回はパスワードでログインするため、sshpassをインストールしておく
[vagrant@master1 vagrant]$ sudo yum install epel-release -y
[vagrant@master1 vagrant]$ sudo yum install sshpass -y --enablerepo=epel
```
- master、node1、node2のプロビジョニング
```bash
[vagrant@master1 ~]$ cd /vagrant
[vagrant@master1 ~]$ ansible-playbook -i inventories/vagrant playbooks/all.yml
[vagrant@master1 ~]$ ansible-playbook -i inventories/vagrant playbooks/master.yml
[vagrant@master1 ~]$ ansible-playbook -i inventories/vagrant playbooks/node.yml

$ vagrant ssh master1
[vagrant@master1 ~]$ sudo kubectl get nodes
NAME      STATUS    ROLES     AGE       VERSION
master1   Ready     master    1m        v1.8.3
node1     Ready     <none>    17s       v1.8.3
node2     Ready     <none>    17s       v1.8.3
```

- k8sを使ってみよう
https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/
