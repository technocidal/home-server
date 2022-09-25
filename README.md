# home-server

## Install Ansible
```
# Create a virtualenv
$ python3 -m venv ~/.venv-ansible

# Activate the virtualenv
$ source ~/.venv-ansible/bin/activate

# Install Ansible
$ pip install ansible

# Deactivate the virtualenv (after your work)
$ deactivate
```

> Credit: https://blog.while-true-do.io/fedora-home-server-automation/

## Usage

Create an inventory (`inventory.ini`) to define which machines you're targeting. 

Execute the following command to deploy `run.yml`.
```
ansible-playbook run.yml
```

## Vault

Create a new keychain item for vault decryption.

```
security add-generic-password \                          
   -a [USER] \
   -s ansible-vault-password \
   -w
```

Edit variables in vault.

```
ansible-vault edit vars/vault.yml
```