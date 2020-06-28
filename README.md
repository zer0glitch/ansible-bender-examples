# ansible-bender-examples

What is ansible-bender?

*Installing ansible-bender

**Fedora

`sudo dnf install -y buildah podman skopeo`

`pip install ansible-bender --user`

**RHEL7 utilizing software collections


**Initializing a project

First we create a project called hello world

```
mkdir hello-world
ansible-bender init
```

The playbook.yml

```
---
- name: Containerized version of $project
  hosts: all
  vars:
    a_variable: value
    # configuration specific for ansible-bender
    ansible_bender:
      base_image: fedora:latest
      target_image:
        # command to run by default when invoking the container
        cmd: /command.sh
        name: $project
      working_container:
        volumes:
        # mount this git repo to the working container at /src
        - "{{ playbook_dir }}:/src"
  tasks:
  - name: install dependencies needed to run project $project
    package:
      name:
      - a_package
      - another_package
      state: present
```



Hello world example


Hello world httpd example


podman commands



