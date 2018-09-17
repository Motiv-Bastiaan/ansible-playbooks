# ansible-playbooks
When you first clone this repo you'll need to prepare your environment to use with Ansible. You can run the following code, assuming you're in the ansible-playbooks directory:
```
# Generate a keypair to use with ansible on the HOST machine
mkdir keys
pwd
ssh-keygen -t rsa -b 4096 #give the keys dir you just created as location for the file, don't use a passphrase

# Create a python venv with ansible on the HOST machine

# Download the files that are too big for github in each roles/*/files directory on the HOST machine

# Create a user that will run the ansible command on the TARGET machine

# Install the PUBLIC key of the pair you just generated in the .ssh directory of the user you just created on the TARGET machine
