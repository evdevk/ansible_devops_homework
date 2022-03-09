### Ansible playbook Add users with loop

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
git clone https://github.com/evdevk/ansible_devops_homework.git && cd ./ansible_devops_homework/lesson2/01_users_loop_add/
```
2. edit hosts and enter there remote server
3. if you are inside playbook folder, run it using:
```
ansible-playbook --vault-password-file=vault_password.txt main.yaml
```

#### Check result
Check users result
```
for i in {1..5}; do id ansible_test$i; done
sudo cat /etc/shadow
sudo cat /etc/passwd
```
