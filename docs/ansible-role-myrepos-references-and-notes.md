#!/bin/bash
#
# 
# install-mr.sh - install mr
#
# * Make executable `chmod +x install-ace.sh`
# * Run `./install-mr.sh`
#
# mr allows you to work with multiple repositories using any version control system including:
#
# * git
# * bzr
# * mercurial
# * darcs
#
# 

# set -

# Change as required

PERSONAL_BIN_DIR="${HOME}/bin"
MR_DIR="${PERSONAL_BIN_DIR}/mr"
BASH_CONFIG_FILE=~/.bashrc
DATE_TIME_STAMP=`date +"%F_%H_%M_%S_%Z"`

# Install requirements

sudo apt-get update
sudo apt-get install -y git
sudo apt-get install -y perl-doc

# Have we already installed mr?

if [ -e "$PERSONAL_BIN_DIR/mr" ]; then
    echo "Found existing $PERSONAL_BIN_DIR/bin"
    echo
    echo "Looks like the mr is already installed"
else
    echo "create personal bin dir"
    mkdir ${PERSONAL_BIN_DIR}
    echo "clone mr"
    cd ${PERSONAL_BIN_DIR}
    git clone https://github.com/joeyh/myrepos.git mr
fi

# append to users shell config file

## backup current version

echo "backing up ${BASH_CONFIG_FILE}."

if [ -f "${BASH_CONFIG_FILE}_ORIGINAL" ]; then
    echo "Found existing ${BASH_CONFIG_FILE}_ORIGINAL"
    echo
    echo "so lets create a timestamped version."
    cp ${BASH_CONFIG_FILE} ${BASH_CONFIG_FILE}_$DATE_TIME_STAMP
else
    echo "backing up ${BASH_CONFIG_FILE} to ${BASH_CONFIG_FILE}_ORIGINAL"
    echo
    cp ${BASH_CONFIG_FILE} ${BASH_CONFIG_FILE}_ORIGINAL
fi

## Making our append

echo ""
echo "appending ${MR_DIR} path to ${BASH_CONFIG_FILE}."
echo "" >> ${BASH_CONFIG_FILE}
echo "# set PATH to include ${MR_DIR}" >> ${BASH_CONFIG_FILE}
echo "if [ -d ${MR_DIR} ] ; then" >> ${BASH_CONFIG_FILE}
echo "    PATH=$PATH:${MR_DIR}" >> ${BASH_CONFIG_FILE}
echo "fi" >> ${BASH_CONFIG_FILE}

echo ""
echo "Restart your terminal"
echo 'Run "mr register" in each repository directory'
echo "that you want to work with using mr"

