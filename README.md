Ansible.Role.VM.InstallPackages
=========

This role install packages from repo  (apt, yum/dnf, pip)

The role can do package reinstallations. In this case, add the package to `packages_to_install` and to `packages_to_remove` at the same time

Language: [EN](README.md), [PL](README.PL.md)

Role Variables
--------------
requires:
```
    os_distribution:       # Linux distribution `CentOS` or `Ubuntu`
    os_version:            # Linux version
    repository_keys:       # Repository keys (only ubuntu)
    repositories:          # Repositories to add or remove
    packages_to_install:   # Packages to install
    packages_to_remove:    # Packages to remove
    pip_packages:          # Packages to install/remove for python
    pip3_packages:         # Packages to install/remove for python3
```

var `repository_keys` example:
```
repository_keys: 
  - name: "Docker"
    url: "https://download.docker.com/linux/ubuntu/gpg"
    state: present
```
var `repositories` example:
```
repositories:
  - name: "Docker"
    repo: "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
    filename: docker
    state: present
```
var `packages_to_install` example:
```
packages_to_install:
  - docker-ce
  - htop
  - apt-transport-https
  - ca-certificates
  - curl
  - software-properties-common
```
var `pip_packages` or `pip3_packages` example:
```
    pip3_packages:
      packages_to_install:
        - docker
        - docker-compose
      packages_to_remove:
        - docker-py
```

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:
```
- hosts: localhost
  remote_user: root
  become: true
  gather_facts: yes
  roles:
    - role: .
      vars:
        repository_keys: 
          - name: "Docker"
            url: "https://download.docker.com/linux/ubuntu/gpg"
            state: present
        repositories:
          - name: "Docker"
            repo: "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
            filename: docker
            state: present
        packages_to_install:
          - docker-ce
          - htop
          - apt-transport-https
          - ca-certificates
          - curl
          - software-properties-common
        pip3_packages:
          packages_to_install:
            - docker
            - docker-compose
          packages_to_remove:
            - docker-py
```

Testing
------------

Testing on:
  - Ubuntu 16.04 LTS
  - Ubuntu 18.04 LTS
  - Ubuntu 20.04 LTS
  - Centos 7
  - Centos 8

License
-------

BSD

Author Information
------------------
 **Maciej Rachuna**
##### System Administrator & DevOps Engineer
rachuna.maciej@gmail.com