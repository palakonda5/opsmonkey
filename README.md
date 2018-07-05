# Title : opsmonkey
### # For this demo i am using Aws  Ubuntu instance
## Requirements

Install ansible 
```
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible
```
# Install docker using ansible
Create docker-install role
```
mkdir roles
 cd roles
 mkdir docker-install
 mkdir tasks
 cd tasks
 ```
 Create a main.yml file using your favorite editor (vi)
 main.yml
 ```
---
- name: Update cache
  apt:
   update_cache: yes
- name: Installing dependencies for docker engine
  apt:
   name: "{{ item }}"
  with_items:
   - apt-transport-https
   - ca-certificates
   - curl
   - software-properties-common
- name:  Add docker GPG Key
  apt_key:
    url: https://download.docker.com/linux/ubuntu/gpg
    state: present
- name: Add Docker APT repository
  apt_repository:
    repo: deb [arch=amd64] https://download.docker.com/linux/ubuntu {{ansible_distribution_release}} stable
- name: Install Docker
  apt: name=docker-ce
```

```
