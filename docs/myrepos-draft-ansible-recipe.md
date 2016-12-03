# myrepos-draft-ansible-recipe.md


## Install requirements

sudo apt-get update
sudo apt-get install -y git
# sudo apt-get install -y perl-doc # is this required??

## ensure for personal bin

## clone myrepos project

cd ~/bin
git clone https://github.com/joeyh/myrepos.git myrepos

## ensure mr executable

chmod +x ~/bin/mr

## ensure for ~/.profile

* if exists backup current

## ensure for ~/.profile entry

```shell

# set PATH so it includes user's private bin if it exists
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi

```

## create link to mr exe in ~/bin

``` shell

ln -s ~/bin/myrepos/mr ~/bin/mr

```

## add myrepos menu entry

```markdown

# myrepos

Manage multiple repositories of any type (git, mercurial, svn...) using single commands

## quick start

* run `mr register` in each repository you wish to track.
* run `mr stat` to see all repository statuses in a directory recursivly.
* run `mr update` to run the equivalent to a `git pull` in all registered repositories contained in a directory.

```

## tests


