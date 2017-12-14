# roles/myrepos/README.md

[![Build Status](https://travis-ci.org/cjsteel/myrepos.svg?branch=master)](https://travis-ci.org/cjsteel/myrepos)
[![Travis CI](http://img.shields.io/travis/csteel/myrepos/default.svg?style=flat)](http://travis-ci.org/csteel/myrepos/default)
[![Platforms](http://img.shields.io/badge/platforms-debian%20/%20ubuntu-lightgrey.svg?style=flat)](#)

## Description

myrepos is an Ansible role used to  

## Recommended

Running Ansible in a virtual environment allows for a lot of testing flexibility.

* [docs/ansible-setup](docs/ansible-setup.md)

## Requirements

* Ansible

## Variables

### project_name/myrepos.yml

* [example_playbook.yml](files/example_playbook.yml)

To install:

```shell
cd project_directory
cp roles/myrepos/files/example_playbook.yml myrepos.yml
# edit if required
nano myrepos.yml
```

### project_name/site.yml

* [example_myrepos.yml](files/example_site.yml)

From the projects main directory run the following:

```yaml
cp roles/myrepos/files/example_playbook.yml myrepos.yml
cat myrepos.yml
```

### project/group_vars/all/project_defaults.yml

[files/group_vars/all/example_defaults.yml](files/group_vars/all/example_defaults.yml)

```yaml
cp roles/myrepos/files/group_vars/all/example_defaults.yml group_vars/all/project_defaults.yml
cat group_vars/all/project_defaults.yml
```

## Testing

Move into the role directory and run vagrant:

```shell
cd roles/myrepos
vagrant up
```

## Authors and License

- [Christopher Steel](http://mcin-cnim.ca/) | [e-mail](mailto:christopher.steel@mcgill.ca)
- [John Le](http://mcin-cnim.ca/) | [e-mail](mailto:john.le@mcgill.ca)
- [Andy Teng](http://mcin-cnim.ca/) | [e-mail](xiaoqiu.teng@mcgill.ca)

License: [MIT](https://tldrlegal.com/license/mit-license)

***
## Open Science

The Neuro has adopted the principles of Open Science. We are inspired by the likes of the Allen Institute for Brain Science, the National Institutes of Health's Human Connectome project, and the Human Genome project. For additional information, please see [Open Science at the Neuro](https://www.mcgill.ca/neuro/open-science-0).

![neuro](imgs/mcin-neuro-logo.png)

  

* ansible-role-myrepos generated using [galaxy-role-skeleton](https://github.com/cjsteel/galaxy-role-skeleton)
