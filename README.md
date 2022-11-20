# ansible_glpi
## Prepare for GLPI-10.0.3 + Fusion-inventory Plugin Installation

This ansible playbook is made on an Ubuntu 22.04 based machine. This playbook will install LAMP stack with GLPI and fusion-inventory plugin. Please follow these steps to prepare your machine and this playbook for installation.

**Step 1:** install ansible through these commands:
-	*sudo apt-add-repository ppa:ansible/ansible*
-	*sudo apt update*
-	*sudo apt install ansible*

**Step 2:** Create default *ansible.cfg* file through these commands:
-	change your current directory to */etc/ansible*
-	define your root password with *sudo passwd root*
-	switch to root user with *su root*
-	create the default *ansible.cfg* file with *sudo ansible-config init --disabled > ansible.cfg*
-	quit root user shell with *exit* command

**Step 3:** prepare your machine for password-based SSH connection (asymmetric):
-	Install OpenSSH on both the controller and the node.

**Step 4:** add your node to hosts file:
-	Open hosts file with *sudo vim /etc/ansible/hosts*
-	Add your hosts alias following his IP address in *ansible_host* parameter. You can add several nodes or create the groups.

**Example:** *glpiserver ansible_host=192.168.1.100*
-	Save your changes and quit the file.

**Step 5:** Create SSH key for your ansible machine user with this command. Remember to create key in non sudo mode and without a passphrase.
-	*ssh-keygen -t ecdsa*

**Step 6:** Download the playbook into your machine (in your home directory for instance) from github:
-	Create a folder named playbook in your home directory
-	Go to the playbook folder
-	Download the playbook form github with …

**Step 7:** Modify default variables if needed in *vars/default.yml*:
-	*app_user* must be the same on the remote machine with the sudo right.
-	Adapt *domain_name* and remote machine’s *hostname* to your environment.

**Step 8:** Create a DNS record in your DNS server following this pattern:
-	*<projet_name>.<domain_name>*
-	For instance: *glpi.mydomain.local*

**Step 9:** lunch the playbook:
-	*ansible-playbook glpi.yml -kbK*
-	Use the SSH (by default same as sudo password) and sudo password for lunch the playbook
-	You can use *--tags=* and *--skip-tags=* to include or exclude tasks from being executed
