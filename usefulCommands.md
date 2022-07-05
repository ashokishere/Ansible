### Install Ansible package using yum on ansible controller
```
sudo yum install epel-release -y ; 
sudo yum install ansible -y
```

### How to execute ansible
```
ansible -m ping all 
# m module
# all - hostname

ansible -a 'cat /etc/hosts' all
ansible -a 'yum install nginx' all --become -become-user nginx
```

### Equivalent to Sudo and change user

```
become: yes
become_user: nginx
```

### Gather facts and other yaml files

gather_facts: yes
--- begin the yaml file or merge mutiple yaml file
{{}} to substitue variable
ansible_password

```
[db_servers]
lamp-db ansible_host=172.20.1.101 ansible_user=maria mysqlservice=mysqld mysql_port=3306 dbname=ecomdb dbuser=ecomuser dbpassword=ecompassword

[web_servers]
lamp-web ansible_host=172.20.1.100 ansible_user=john httpd_port=80 repository=https://github.com/kodekloudhub/learning-app-ecommerce.git
```

```
 [db_servers]
lamp-db ansible_host=172.20.1.101 ansible_ssh_private_key_file=/home/thor/.ssh/maria ansible_user=maria mysqlservice=mysqld mysql_port=3306 dbname=ecomdb dbuser=ecomuser dbpassword=ecompassword

[web_servers]
lamp-web ansible_host=172.20.1.100 ansible_ssh_private_key_file=/home/thor/.ssh/john ansible_user=john httpd_port=80 repository=https://github.com/kodekloudhub/learning-app-ecommerce.git
````

### Modules

packages To isntall packages like httpd, 
service  managing a services start,stop enable
firewalld   port,ip, zone
lvg : create volume group
filesystem : to create filesysmte
mount : to mount file system
file :  to create and permisssion files
Archive : to compress files and folders
unarchive : to decompress the files and folders
Cron : schedule a task
user : to create users
group : to create groups
authorized_keys : to push th ekeys

### Create a playbook httpd.yml under ~/playbooks/ to install httpd package on web1 node using Ansible’s yum module.

```
--
- hosts: web1
  tasks:
  - name: Install httpd package
    yum: name=httpd state=installed

```


### We have an rpm available for wget package on URL http://mirror.centos.org/centos/7/os/x86_64/Packages/wget-1.14-18.el7_6.1.x86_64.rpm. Create a playbook with name wget.yml under ~/playbooks to install that rpm on web1 node using yum module.

```
---
- hosts: web1
  tasks:
  - yum:
      name: http://mirror.centos.org/centos/7/os/x86_64/Packages/wget-1.14-18.el7_6.1.x86_64.rpm
      state: present

```

### o install unzip package on web1 node. We want to install unzip-5.52 version of this package so before running the playbook make the required changes.

```
---
- hosts: all
  tasks:
    - name: Install unzip package
      yum:
        name: unzip-5.52
        state: present


```
### Our playbook - iotop.yml - to install the latest version of iotop package keeps failing. Please fix the issue so that playbook can work


The playbook is located under ~/playbooks directory. And the inventory file is inventory

```
---
- hosts: all
  tasks:
    - name: Install iotop package
      yum:
        name: iotop
        state: latest


```




