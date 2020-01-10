# Ansible

### Install
```
brew install ansible # for Mac
sudo yum install ansible # for CentOS
sudo apt-get ansible # Ubuntu
```

### Quick Start
* `ansible localhost -m ping`
* `ansible all -i host/front -m ping`
* `ansible all -i host/front -l first -m ping`
* `ansible all -i host/front -l first,second -m ping`
* `ansible all -i host/front -l first -a "echo hello"`
* `ansible all -i host/front -l first -m shell -a "grep sth /mydir/logs/application.log"`
* Host Key 체크하지 않도록 설정
```
// vi ansible.cfg
[defaults]
host_key_checking = False
```

### Option
* -i : Inventory
* -l : Subset
* -m : Module
* -a : Arguments

### Inventory
* INI
```
[agroup]
test1.com

[bgroup]
test[2:5].com
test[a:c].com ansible_connection=ssh ansible_user=someone http_port=80 maxRequestsPerChild=808

[bgroup:vars]
ntp_server=ntp.atlanta.example.com
proxy=proxy.atlanta.example.com
```
* YAML
```
all:
  hosts:
    mail.example.com:
  children:
    webservers:
      hosts:
        foo.example.com:
        bar.example.com:
    dbservers:
      hosts:
        one.example.com:
        two.example.com:
        three.example.com:
```

### Playbook
* Simple
```yml
- name : Quick Start
  hosts : all
  tasks :
    - name : Make temporary directory
      shell : "mkdir -p /home/deploy/tmp"
```
`ansible-playbook playbooks/simple.yml -i host/front`
`ansible-playbook playbooks/simple.yml -i host/front -l first`
