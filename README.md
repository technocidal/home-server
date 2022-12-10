# home-server

## Install Ansible

```bash
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

Install all 3rd party roles this playbook uses.

```bash
ansible-galaxy install -r requirements.yml
```

Create an inventory (`inventory.ini`) to define which machines you're targeting. 

Execute the following command to deploy `run.yml`.

```bash
ansible-playbook run.yml
```

## Vault

Create a new keychain item for vault decryption.

```bash
security add-generic-password \                          
   -a [USER] \
   -s home-server-vault \
   -w
```

Edit variables in vault.

```bash
ansible-vault edit vars/vault.yml
```

## Knowledgebase

### Homebridge

This Homebridge setup is quite unusual. I've learned a lot from
this [blog article](https://www.devwithimagination.com/2020/02/02/running-homebridge-on-docker-without-host-network-mode/).
Run the `generate-services.sh` on the server to generate a avahi service definition for
everything that runs inside the homebridge container. SELinux will complain about
avahi trying to access that the generated file. 
Run the following commands to fix those permissions.

```bash
# Generate policy
ausearch -c 'avahi-daemon' --raw | audit2allow -M my-avahidaemon
# Apply policy
semodule -i my-avahidaemon.pp
# Restart avahi
sudo systemctl restart avahi-daemon.service
```

HomeKit also seems to have problems picking up new accessories added to Homebridge.
You can fix this by removing Homebridge from HomeKit via Home.app, [resetting Homebridge](https://github.com/homebridge/homebridge/wiki/Connecting-Homebridge-To-HomeKit#how-to-reset-homebridge), generating a new services definition for avahi and repairing Homebridge.
