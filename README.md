# ansible-playbooks
When you first clone this repo you first need to create a keypair to use with Ansible. You can run the following code, assuming you're in the ansible-playbooks directory:
```
# Generate a keypair to use with ansible
mkdir keys
pwd
ssh-keygen -t rsa -b 4096 #give the keys dir you just created as location for the file, don't use a passphrase

# Download the file that are too big for github in each roles/*/files directory

# Create a user that will run the ansible command on the TARGET machine

