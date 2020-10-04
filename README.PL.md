Ansible.Role.VM.InstallPackages
=========

Rola instalująca paczki z repozytorium (apt, yum/dnf, pip)

Rola może zrobić reinstalacje paczki. W tym przypadku należy dodać pakiet do `packages_to_install` i jednocześnie do `packages_to_remove`

Język: [EN](README.md), [PL](README.PL.md)

Zmienne w roli
--------------
requires:
```
    os_distribution:       # Wersja dystrybucji `CentOS` or `Ubuntu`
    os_version:            # Wersją systemu
    repository_keys:       # Lista Repozytorium kluczy (only ubuntu)
    repositories:          # Lista Repozytoria
    packages_to_install:   # Lista paczek do zainstalowania
    packages_to_remove:    # Lista paczek do usuniecia
    pip_packages:          # Lista moudułów pytahona do zainstalowania
    pip3_packages:         # Lista moudułów pytahona do zainstalowania (python3)
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

Przykładowy Playbook
----------------

Przykładowy playbook
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

Testowanie
------------

Testing on:
  - Ubuntu 16.04 LTS
  - Ubuntu 18.04 LTS
  - Ubuntu 20.04 LTS
  - Centos 7
  - Centos 8

Licencja
-------

BSD

Autor
------------------
 **Maciej Rachuna**
##### System Administrator & DevOps Engineer
rachuna.maciej@gmail.com