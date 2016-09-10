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

Description of the settable variables including those that can/should be set via parameters to the role.

### defaults/main.yml
 
    ---
    # defaults file for ansible-role-myrepos
    
    myrepos_myrepos_source_repository: 'https://github.com/csteel/myrepos'
    myrepos_uid_min                  : 1000
    myrepos_uid__max                 : 60000
    myrepos_bin_dir                  : 'bin/myrepos'

### vars/main.yml

  Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

### Basic

This role playbook is included in the roles []( files/myrepos.yml )


```yaml
---
- hosts: myrepos
  become: true
  gather_facts: true
  roles:
- myrepos
```

### Using variables passed in as parameters

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

MIT

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
