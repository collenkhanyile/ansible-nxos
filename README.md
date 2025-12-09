# ansible-nxos
Automatic cisco nexus

running automation on a network lab was present with issues.

Make sure that you are running the commands for the known user if switch uses you might exprience below error white interacting with the newtork.

Network diagram:
<img width="767" height="690" alt="image" src="https://github.com/user-attachments/assets/d847bc18-0c9a-4658-b33d-3cf2d85ee214" />


<img width="961" height="112" alt="image" src="https://github.com/user-attachments/assets/5234957e-06d2-4463-94b2-e3ed42b3ddb8" />

<img width="1525" height="184" alt="image" src="https://github.com/user-attachments/assets/36051e34-34ee-423d-9712-18902fe5f1a1" />

# ssh key issues how to resolve.

 METHOD 1 — Use ssh-keyscan (recommended)

This is the simplest way to add a host key manually without connecting interactively.

Add key to known_hosts
ssh-keyscan 10.0.0.208 >> ~/.ssh/known_hosts # make sure your keys are stored in the correct location # run this command to confirm the correct location :ssh admin@10.0.0.208 -v

get the content of this file:
cat /home/workernode/.ssh/id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQ.... worknode

# Add the configuration to your Cisco devices.
username admin sshkey ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQ.... worknode
