Ansible-NXOS Automation Report Automated Configuration of Cisco Nexus Devices This document provides an overview of the issues encountered and the solutions implemented while running Ansible-based automation on a Cisco Nexus network lab environment.

Overview During the deployment of automation tasks on a Cisco Nexus lab environment, several SSH authentication and host-key validation issues were encountered. These errors typically occur when interacting with devices that do not yet exist in the local known_hosts file or when incorrect keys are used. The following sections outline the problem, the environment, and the recommended corrective actions.

Network Topology The automation was executed against the lab network shown below:

image
Common SSH Host Key Issues When attempting to connect to a Nexus device for the first time, you may encounter warnings such as:
image image
Host authenticity cannot be established

Bad server host key

Invalid key length

These issues occur when the host key is missing or mismatched in ~/.ssh/known_hosts.

Resolution: Adding SSH Host Keys Method 1 — Using ssh-keyscan (Recommended) This is the most reliable and non-interactive method to add a device’s SSH host key to your local known_hosts file. Step 1: Scan and add the host key ssh-keyscan 10.0.0.208 >> ~/.ssh/known_hosts
Note: Ensure that you are using the correct .ssh directory for the user executing Ansible. To verify the key path and SSH behavior, run:

ssh admin@10.0.0.208 -v

Step 2: Retrieve Your Public Key Confirm the public key that will be used for authentication: cat /home/workernode/.ssh/id_rsa.pub

Example output: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQ.... worknode

Step 3: Add the SSH Key to the Cisco Nexus Device On the Nexus device configuration, add your Ansible control-node public key: username admin sshkey ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQ.... worknode

This ensures passwordless authentication and prevents repeated host-key prompts.

Conclusion By properly registering host keys and ensuring the correct SSH key configuration on both the Ansible control node and the Nexus switches, all automation tasks executed successfully without further SSH authentication errors. If you need this formatted specifically for a PDF, Markdown, or project documentation standard, feel free to ask!
