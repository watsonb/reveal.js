1. swap the docker install with the podman install

students will be using rhel 8

yum module install container-tools

This gives them podman (and other tools like skopeo, buildah)

have them run docker <blah> and then do below

yum install podman-docker


Delete the python install slide


## student machine provisioning

```bash
ssh watsonb@dev03.dinohead.com
sudo su - ansible
podman ps -a
   14  podman rm ansible
   15  podman run --name=ansible -it -v ~/workspace/ansible/ansible_environments/:/root/workspace/ansible/ansible_environments:Z -v ~/workspace/ansible/ssh_keys:/root/workspace/ansible/ssh_keys:Z -v ~/workspace/ansible/ansible.cfg:/root/workspace/ansible/ansible.cfg:Z -v ~/workspace/ansible/ansible_vaults:/root/workspace/ansible/ansible_vaults:Z docker.io/dinohead/ansible:v2 /bin/bash
```


root history in running container

```bash
[root@dea69abd63e5 ansible]# history
    1  vim /root/.ssh/id_rsa
    2  pymgit -r /root/workspace/repos.yml -g
    3  source ~/venv_pymgit/bin/activate
    4  pymgit -r /root/workspace/repos.yml -g
    5  rm ~/.ssh/id_rsa 
    6  exit
    7  ls
    8  ls ansible_environments/
    9  ls ansible_environments/ae_dinohead.com/
   10  ls ansible_vaults/
   11  cat ansible.cfg 
   12  ls
   13  pwd
   14  ansible-playbook ansible_playbooks/dinohead/ap_dinohead_playbooks/development_host.yml -i ansible_environments/ae_dinohead.com/student.yml -e variable_host=*08*
   15  ansible-playbook ansible_playbooks/dinohead/ap_dinohead_playbooks/development_host.yml -i ansible_environments/ae_dinohead.com/student.yml -e variable_host=*08*
   16  cat ansible.cfg 
   17  vim ansible.cfg 
   18  ansible-playbook ansible_playbooks/dinohead/ap_dinohead_playbooks/development_host.yml -i ansible_environments/ae_dinohead.com/student.yml -e variable_host=*08*
   19  ssh student@student08.dinohead.com
   20  history
```