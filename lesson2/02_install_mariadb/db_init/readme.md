### Ansible playbook Nginx with SSL

Simple playbook to create users with loop using vault encrypting

### Requirements and recommendations:

##### Hosts:

1. 2 Virtual servers. One for running ansible playbook and one for nginx
2. Centos 7.9.2009 minimal - both host for ansible and host for nginx running on VirtualBox (VB NAT + Virtual host adapter for working connection between VB hosts)
[Link to Centos images](http://isoredirect.centos.org/centos/7/isos/x86_64/)
3. Access to internet
4. SELinux in permissive mode
5. Firewalld installed and enabled, opened 22 port on both hosts
6. User ansible on both hosts with SUDO NO PASSWD
```
cat /etc/sudoers:
 ansible ALL=(ALL) NOPASSWD:ALL
```
7. Host for ansible:
```
ssh ansible@host
sudo yum install python3 pip
cd 
python3 -m venv ./ansivenv && source ./bin/activate
```
8. Host for nginx:
```
sudo yum install python2
```

#### How to run
1. Create virtual environment, clone project, locate to playbook folder:
```
cd ~ && source .ansivenv/bin/activate
git clone https://github.com/evdevk/ansible_devops_homework.git && cd ./ansible_devops_homework/lesson2/02_install_mariadb/db_init
```
2. edit hosts and enter there remote server
3. if you are inside playbook folder, run it using:
```
ansible-playbook main.yaml
```

#### Check result
Use commands on a remote server with mariadb
```
mysqladmin -u root -proot_pass123 status
mysql -u root -proot_pass123 -h localhost -e "select host, user, password from mysql.user;"
mysql -u ansible_user -pansible_pass123 -e "DROP TABLE IF EXISTS ansible_db.mytable; \
 CREATE TABLE ansible_db.mytable (a int);"
```