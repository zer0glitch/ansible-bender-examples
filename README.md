# ansible-bender-examples

What is ansible-bender?

*Installing ansible-bender*

**Fedora**

`sudo dnf install -y buildah podman skopeo`

`pip install ansible-bender --user`

**RHEL7 utilizing software collections**


The playbook.yml

```
---
# the task name, can be set to an string
- name: Containerized version of hello-world
  hosts: all
  vars:
    # random variables can be assigned just as any other ansible vars definition
    a_variable: value
    # configuration specific for ansible-bender
    ansible_bender:
      # the docker base image, the default is fedora:latest for the purpose
      # of our project we are utilizing the Red Hat ubi images
      base_image: fedora:latest
      target_image:
        # command to run by default when invoking the container
        cmd: /command.sh
        # the name of the image produced
        name: hellow-world
      working_container:
        volumes:
        # mount this git repo to the working container at /src
        - "{{ playbook_dir }}:/src"
  tasks:
  - name: installing packages
    package:
      name:
      - a_package
      - another_package
      state: present
```



Hello world example
**Initializing a project**

First we create a project called hello world, and then run the ansible-bender init to create our base playbook.yml

```
mkdir hello-world
cd hello-world
ansible-bender init
```



Hello world httpd example


podman commands



