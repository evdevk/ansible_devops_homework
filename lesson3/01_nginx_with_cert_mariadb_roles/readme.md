### Ansible playbook Nginx with SSL

Ansible roles:

* generate selfsigned certificate
* install Nginx with SSL support
* install MariaDB with additional user and database

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

#### How to run all

1. Create virtual environment, clone project, locate to playbook folder:

```
cd ~ && source .bin/activate
python3 -m pip install --upgrade pip && python3 -m pip install ansible==2.9.14
ansible-galaxy collection install community.crypto
git clone https://github.com/evdevk/ansible_devops_homework.git && cd ./ansible_devops_homework/lesson2/02_install_mariadb/db_init
```

2. edit hosts and enter there remote server
3. edit var/settings.yml if you need
4. if you are inside playbook folder, run it using:

```
ansible-playbook main.yaml
```
<br>
###### Tags:

**generate\_cert**  - Generate certificate with test
**generate\_cert\_test** \- Test certificate validation only
**mariadb\_install** \- Install and test MariaDB
**mariadb\_check** \- Test mariaDB with user and password only
**nginx\_install** \- Install and test Nginx
**nginx\_check** \- Test Nginx only
**nginx\_tls\_install** \- Generate cert\, install Nginx and test

#### **Run with tags**
```
Install only mariadb:
ansible-playbook main.yaml --tags mariadb_install

Install only nginx:****
ansible-playbook main.yaml --tags nginx_tls_install

Only generate cert:
ansible-playbook main.yaml --tags generate_cert

Only test all:
ansible-playbook main.yml --tags generate_cert_test,mariadb_check,nginx_check
```
