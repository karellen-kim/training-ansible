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
* `ansible all -i host/front -l alpha -m ping`
* `ansible all -i host/front -l alpha,sandbox -m ping`
* `ansible all -i host/front -l alpha -a "echo hello"`
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
```
[agroup]
test1.com

[bgroup]
test[2:5].com
test[a:c].com ansible_connection=ssh ansible_user=someone
```

