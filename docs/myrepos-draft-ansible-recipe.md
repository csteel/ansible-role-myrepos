# myrepos-draft-ansible-recipe.md

# Variables

# define the range of uid's we are interested in.

## Users

myrepos_uid_min: 1001
myrepos_uid_max: 1001

## Files

myrepos_myrepos_bin_dir: 'myrepos'

## Install requirements

sudo apt-get update
sudo apt-get install -y git
# sudo apt-get install -y perl-doc # is this required??

# ensure for personal bin

## Create a list of user names on the target system.

- name: "get remote systems users within a designated UID range"
  shell: >
    awk -F':' -v "min={{ myrepos_uid_min }}" -v "max={{ myrepos_uid_max }}" '{ if ( $3 >= min && $3 <= max ) print $0}' /etc/passwd | cut -d: -f1
  changed_when: false
  register: users_in_uid_range

## Retrieve home directories for users in our designated UID range.

- name: "discover home directories including those mounted by LDAP"
  shell: >
    getent passwd {{ item }} | cut -d: -f6
  changed_when: false
  register: user_homes
  with_items: users_in_uid_range.stdout_lines

## ensure tartget users have a personal bin directory

- name: "ensure for ~/bin for users in our uid range"

  become: true
  file:
    state   : 'directory'
    path    : '{{ item.stdout }}/bin'
    owner   : '{{ item.stdout | basename }}'
    group   : '{{ item.stdout | basename }}'
    mode    : '0740'
  with_items: "{{ user_homes.results }}"

## clone myrepos project

# equivalent
# cd ~/bin
# git clone https://github.com/joeyh/myrepos.git /home/<username>myrepos

# Example git checkout from Ansible Playbooks
- git:
    repo: 'https://github.com/csteel/myrepos.git'
    dest: '{{ item.stdout }}/bin/{{ myrepos_myrepos_bin_dir }}'
    reference: no # Reference repository (see "git clone --reference ...")
    remote: origin
    track_submodules: no
    update: yes
    version: 1.20160123
  with_items: "{{ user_homes.results }}"

## ensure mr executable

chmod +x ~/bin/mr

- file:
    path: '{{ item.stdout }}/bin/{{ myrepos_myrepos_bin_dir }}'
    owner   : '{{ item.stdout | basename }}'
    group   : '{{ item.stdout | basename }}'
    mode: 0755
  with_items: "{{ user_homes.results }}"

## ensure for ~/.profile

* if exists backup current

- name: 'when ansible_distribution == "CentOS", template our menu script'
  become: true
  template:
    backup  : yes
    src     : '{{ ansible_distribution }}/{{ ansible_distribution_major_version }}/home/.profile.j2'
    dest    : '{{ item.stdout }}/.profile'
    owner   : '{{ item.stdout | basename }}'
    group   : '{{ item.stdout | basename }}'
    mode    : '0740'
  with_items: "{{ user_homes.results }}"
#  when: ansible_distribution == "CentOS" 

## ensure for ~/.profile entry

```shell

# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi


```

- name: "ensure for our path block in ~/.profile"
  become: true
  blockinfile:
    dest    : '{{ item.stdout }}/.profile'
    owner   : '{{ item.stdout | basename }}'
    group   : '{{ item.stdout | basename }}'
    mode    : '0644'
    state   : 'present'
    marker  : '# {mark} ANSIBLE MANAGED BLOCK'
    block: |
      # set PATH so it includes user's private bin if it exists
      if [ -d "$HOME/bin" ] ; then
          PATH="$HOME/bin:$PATH"
      fi
  with_items: "{{ user_homes.results }}"
#  when: ansible_distribution == "Ubuntu" 

## create link to mr exe in ~/bin

``` shell

ln -s ~/bin/myrepos/mr ~/bin/mr

```

- file:
    src     : '{{ item.stdout }}/bin/{{ myrepos_myrepos_bin_dir }}/mr'
    dest    : '{{ item.stdout }}/bin/mr'
    owner   : '{{ item.stdout | basename }}'
    group   : '{{ item.stdout | basename }}'
    mode    : 0755
    state   : link
  with_items: "{{ user_homes.results }}"

## add myrepos menu entry

### add one workd item title to ~/bin/acemenu/menuitems.txt

echo "myrepos" > ~/bin/acemenu/menuitems.txt

### Create contents of ~/bin/acemenu/helpfiles/myrepos.txt
```markdown

# myrepos

Manage multiple repositories of any type (git, mercurial, svn...) using single commands

## quick start

* run `mr register` in each repository you wish to track.
* run `mr stat` to see all repository statuses in a directory recursivly.
* run `mr update` to run the equivalent to a `git pull` in all registered repositories contained in a directory.

```

## tests

### check myrepos version command.
mr --version

