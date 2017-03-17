
ansible-role-myrepos
====================

ansible-role-myrepos is an Ansble role that can be used to install and configure **myrepos** for one or more users personal ~/bin directory(s).

Description
-----------

myrepos is a tool that allows you to manage all your version control repositories. The `mr` command can be used to update all of your repositories at once, push out all your local changes and more. It can support any version control system and provides out of the box support for git, svn, mercurial, bzr, darcs, cvs, fossil and veracity.


References
----------

* [ getting started with myrepos ]( https://myrepos.branchable.com/ )
* [ https://github.com/joeyh/myrepos ]( https://github.com/joeyh/myrepos )


Requirements
------------

Pre-requisites not covered by Ansible itself include:

* One or more installed version control systems.
* [ Ansible role ensure_dirs ]( https://github.com/csteel/ansible-role-ensure_dirs )


Role Variables
--------------

###  group_vars/myrepos/myrepos_defaults.yml

```shell
mkdir -p group_vars/myrepos
cp roles/myrepos/files/group_vars/myrepos/myrepos_defaults.yml group_vars/myrepos/.
```

#### content example

```shell
```

### defaults/main.yml

```yaml
```

Dependencies
------------

* [csteel/ansible-role-ensure_dirs](https://github.com/cjsteel/ansible-role-ensure_dirs)
* [cjsteel/ansible-role-skel](https://github.com/cjsteel/ansible-role-skel)

### myrepos/meta/main.yml

See this file for dependancies example

Example Playbook
----------------

### Basic role playbook

[ files/myrepos.yml ]( files/myrepos.yml ) is an example of a working playbook for this role  that can be included in a main playbook.

```shell
cp roles/myrepos/files/myrepos.yml .
```

Example

```yaml

---
# file: myrepos.yml

- hosts: myrepos
  become: true
  gather_facts: true 
  roles:
    - myrepos
```

### Main playbook

The main playbook might look something like this:

```yaml

# file: systems.yml

- hosts: all
  become: false
  gather_facts: false

- include: myrepos.yml

```

### Using variables passed in as parameters

This example would only install myrepo for the user with the uid of 1001

```yaml

---
- hosts: myrepos
  become: true
  gather_facts: true
  roles:
     - { myrepos, myrepos_min_uid: 1001, myrepos_max_uid: 1001 } 
```


License
-------

MIT

Author Information
------------------

Christopher Steel  
Systems Administrator  
McGill Centre for Integrative Neuroscience  
Montreal Neurological Institute  
McGill University  
3801 University Street  
Montréal, QC, Canada H3A 2B4  
Tel. No. +1 514 398-2494 
E-mail: christopherDOTsteel@mcgill.ca  
[MCIN](http://mcin-cnim.ca/), [theneuro.ca](http://theneuro.ca)  

