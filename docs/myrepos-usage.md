# file: mr usage.md

## mr

Allows you to work with multiple repositories using any version control system including:

* git, or bzr, mercurial or darcs

### Resources

* [](http://myrepos.branchable.com/)
* [github.com/joeyh/myrepos](https://github.com/joeyh/myrepos)

### Requirements

* Multiple repositories that you work with.

### Recommendation / Best practices?

* Use SSH Key pairs for repositories
* Use SSH agent

### mr register

* run mr register in each repository (should we start with deepest nested?
* This  That sets up a ~/.mrconfig file listing your repositories.

    cd repo
    mr register
    cat ~/.mr 

### mr status

Any of the following give you the status of all your repositories. Run it from you hom,e directory for an overview of any repositories in your home (no matter what directory they are in.

    cd ~
or
    cd projects
then
    mr sta
    mr stat
    mr status

### mr update

    cd ~
    mr up
run mr update in your home directory, and it'll update every one of your repositories that you've registered with myrepos.

Want to update repositories in parallel? mr -j5 update will run 5 concurrent jobs!

If you run mr update inside a repository, it'll only act on that repository. In general, any mr command runs recursively over any repository located somewhere in or under the current directory.

You can also run mr commit, mr push, mr status, mr diff, and a lot of other commands. These work no matter which version control system is used for a repository. Of course, you can still use the native version control commands too.

Oh, and you can abbreviate any command to any unambiguous abbreviation. mr up, mr pu, etc.

Now, maybe you find that you always want to update one repository using git pull --rebase, instead of the default git pull that mr update runs. No problem: The ~/.mrconfig file makes it easy to override the command run for any repository. It's like a Makefile for repositories.

####

[foo]
checkout = git@github.com:joeyh/foo.git
update = git pull --rebase

You can make up your own commands too:

[bar]
# This repository has an upstream, which I've forked; 
# set up a remote on checkout.
checkout = 
    git clone git@github.com:joeyh/bar.git
    cd bar
    git remote add upstream git@github.com:barbar/bar.git
# make `mr zap` integrate from upstream
zap = 
    git pull upstream
    git merge upstream/master
    git push origin master

You can even define commands globally, so mr can use them in all repositories.

[DEFAULT]
# Teach mr how to `mr gc` in git repos.
git_gc = git gc "$@"

This only scratches the surface of the ways you can use myrepos to automate and mange your repositories!

Some more examples of things it can do include:

    Update a repository no more frequently than once every twelve hours.
    Run an arbitrary command before committing to a repository.
    Remember actions that failed due to a laptop being offline, so they can be retried when it comes back online.
    Combine several related repositories into a single logical repository, with its own top-level .mrconfig file that lists them and can be chain loaded from ~/.mrconfig.
    Manage your whole home directory in version control. (See VCS-Home)

news
