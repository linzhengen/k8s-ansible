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
- master1で管理用ユーザを作成してから、sshキーを撒く
```bash
[vagrant@master1 ~]$ cd /vagrant
[vagrant@master1 ~]$ ansible-playbook -i inventories/vagrant/default playbooks/secure.yml
```

- provisionになって、playbooks/all.ymlを実行する
```bash
[vagrant@master1 ~]$ sudo su provision -
[provision@master1 vagrant]$ ansible-playbook -i inventories/vagrant playbooks/all.yml
```








 