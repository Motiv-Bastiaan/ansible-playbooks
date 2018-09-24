# ansible-playbooks

## Preparing the environment
When you first clone this repo you'll need to prepare your environment to use with Ansible, this will not work on Windows. You can run the following code:
```
# First clone the repo
git clone https://github.com/Motiv-Bastiaan/ansible-playbooks.git
# Goto the newly created dir
cd ansible-playbooks/
# Generate a keypair to use with ansible on the HOST machine
mkdir keys
pwd
ssh-keygen -t rsa -b 4096 #give the keys dir you just created as location for the file, don't use a passphrase

# Create a python venv with ansible on the HOST machine
# Depending on your environment you might need to 
# UBUNTU 
# enable ubuntu universe repository (sudo add-apt-repository universe), install python virtualenv (sudo apt-get install python3-venv), install python dev (sudo apt install python3-dev) or add python to your path.
python3 -m venv ansiblevenv
# CentOS
# install python3 sudo yum install rh-python36, enable Software Collections sudo yum install centos-release-scl, install dev tools sudo yum groupinstall 'Development Tools'
scl enable rh-python36 bash
python -m venv ansibleenv
# Now activate the Python virtual environment
source ./ansiblevenv/bin/activate
# Upgrade pip to the lastest version
pip install --upgrade pip
# And install ansible
pip install ansible

# Download the files that are too big for github in each roles/*/files directory on the HOST machine
source download_files

# Create a user that will run the ansible commands on the TARGET machine
sudo useradd -m sa_ansible
# And add it to the sudoers file
sudo visudo #Below the %sudo entry add
sa_ansible ALL=(ALL) NOPASSWD:ALL

# Install the PUBLIC key of the pair you just generated in the authorized_keys file of the user you just created on the TARGET machine
sudo mkdir /home/sa_ansible/.ssh
vi /home/sa_ansible/.ssh/authorized_keys
sudo chown -R sa_ansible:sa_ansible /home/sa_ansible/.ssh
# Paste the PUBLIC key in this file
cat keys/id_rsa.pub # On the HOST

# Make sure python is installed on the TARGET machine
python # You should see the python promt if not install (sudo apt install python)

# Make sure openssh server is installed and running on the TARGET machine
sudo systemctl status sshd # Active: should say active(running) (install with sudo systemctl status sshd)

# Now we can test the connectivity
# First activate the ansible venv
source ansiblevenv/bin/activate
# Now run an Ansible ping
ansible all -i inventory -m ping #Where inventory is the inventory file
```

## Create the inventory file

