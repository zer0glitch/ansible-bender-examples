# ansible-bender-examples

Links
[ansible-bender](b)
[Red Hat ubi images](https://www.redhat.com/en/blog/introducing-red-hat-universal-base-image)

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
mkdir hello-world2
cd hello-world2
ansible-bender init
```

Modify the hello-world2/playbook.yml, use the hello-world/playbook.yml as an example

Build the playbook

`cd hello-world2`

Build the image

`ansible-bender build playbook.yml`


View the images

`podman images`


```
REPOSITORY                            TAG      IMAGE ID       CREATED          SIZE
localhost/hello-world2                latest   797eb1160945   11 seconds ago   215 MB
<none>                                <none>   26b0a5c76fce   14 seconds ago   215 MB
<none>                                <none>   2c7bd99cae56   2 minutes ago    215 MB
<none>                                <none>   2e8bbbd8218f   2 minutes ago    215 MB
registry.access.redhat.com/ubi7/ubi   latest   be486c8f3852   11 days ago      215 MB
```

Run an image using podman

`podman run localhost/hello-world2:latest`

By default the system will print out `Hello you`, `you` is default for the enviornment variable `NAME`.  If we would like to set the variable `NAME` this can be done by passing the environment variable during the `podman run` command

`podman run --env 'NAME=Mickey' localhost/hello-world2:latest`

You can also define a set of variables in a file.

***Create a file named my.envs***
`vim my.envs`

Add a line to set the name variable

`NAME=MickeyFromFile`

`podman run --env-file my.envs localhost/hello-world2:latest`


You will see the newly created image


Hello world httpd example


podman commands







