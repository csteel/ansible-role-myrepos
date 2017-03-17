
Role Name
=========

Myrepos is an Ansble role to install and configure **myrepos** for one or more users personal ~/bin directory(s). It gathers users home directories using 


Description
-----------

myrepos is a tool that allows you to manage all your version control repositories. The `mr` command can be used to update all of your repositories at once, push out all your local changes and more. It can support any version controll system and provides out of the box support for git, svn, mercurial, bzr, darcs, cvs, fossil and veracity.


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
---
# file: group_vars/myrepos/myrepos_defaults.yml

myrepos_repo: "https://github.com/geerlingguy/myrepos.git"
myrepos_repo_accept_hostkey: no
myrepos_repo_local_destination: "~/Documents/myrepos"


myrepos_remote_directories:

  myrepos_home
   
    state   : "directory"
    path    : "relatve/subdir"
    owner   : "bob"
    group   : "sales"
    mode    : "0750"
    recurse : "true"

myrepos_home: "~/bin/mr"
myrepos_
myrepos_files:
  - .bash_profile
  - .gitignore
  - .inputrc
  - .vimrc

#PERSONAL_BIN_DIR="${HOME}/bin"
#MR_DIR="${PERSONAL_BIN_DIR}/mr"
#BASH_CONFIG_FILE=~/.bashrc
#DATE_TIME_STAMP=`date +"%F_%H_%M_%S_%Z"`

```



group_vars/myrepos/myrepos_defaults.yml

Description of the settable variables including those that can/should be set via parameters to the role.

### defaults/main.yml

```yaml

---
# defaults file for ansible-role-myrepos

myrepos_myrepos_source_repository: 'https://github.com/csteel/myrepos'
myrepos_uid_min                  : 1000
myrepos_uid__max                 : 60000
myrepos_bin_dir                  : 'bin/myrepos'


### group_vars/developer/myrepos_defaults

### host_vars/<host_name>/myrepos_users.yml



​```yaml

# file: host_vars/<host_name>/myrepos_users.yml

myrepos_myrepos_source_repository: 'https://github.com/csteel/myrepos'
myrepos_system_myrepos_users     : []
myrepos_uid_min                  : 1000
myrepos_uid__max                 : 60000
myrepos_bin_dir                  : 'bin/myrepos'
```


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

### Basic role playbook

[ files/myrepos.yml ]( files/myrepos.yml ) is an example of a working playbook for this role  that can be included in a main playbook.


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

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
