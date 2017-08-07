* add `mr register` option to tasks/main.yml
* use mr register as dependancy for installing other clones and would create

/etc/skel/.mrconfig

## /etc/skel/.mrconfig content example

[bin/acemenu]
checkout = git clone 'git@github.com:cjsteel/ansible-role-acemenu.git' 'acemenu'

# Variables

