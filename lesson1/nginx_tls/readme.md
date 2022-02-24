### Ansible playbook Nginx with SSL

Simple playbook to install nginx with selfsigned SSL support.

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
1. cd ~ && source .ansivenv/bin/activate
2. git clone && cd ./123
3. edit hosts and enter there nginx server
4. ansible-playbook main.yaml

#### Check result
open in browser
```
http://<host>
https://<host>
```
