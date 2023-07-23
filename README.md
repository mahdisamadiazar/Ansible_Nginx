# Ansible_Nginx
run Nginx using docker compose in Ansible

### Install ansible on server
apt update
apt install software-properties-common
apt-add-repository --yes --update ppa:ansible/ansible
apt install ansible

####install docker and docker compose
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo apt-get upgrade
sudo curl -L "[https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname ↗](https://github.com/docker/compose/releases/download/1.29.2/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

#Create a new directory for your Ansible project:
mkdir my_ansible_project

#Change into the new directory:
cd my_ansible_project

#clone dockercompose.yml from https://github.com/mahdisamadiazar/Ansible_Nginx.git
git clone https://github.com/mahdisamadiazar/Ansible_Nginx.git

#Create a new file with a .yml extension for your Ansible playbook:
touch my_playbook.yml

#Open the my_playbook.yml file in a text editor and define the tasks for your playbook. Here is an example:
---
- name: Deploy Docker Compose project
  hosts: all
  become: true
  vars:
    project_name: my_project
    project_path: /path/to/my_project

  tasks:
    - name: Install Docker Compose
      apt:
        name: docker-compose
        state: present

    - name: Copy Docker Compose file
      copy:
        src: docker-compose.yml
        dest: "{{ project_path }}/docker-compose.yml"

    - name: Start Docker Compose project
      community.general.docker_compose:
        project_src: "{{ project_path }}"
        project_name: "{{ project_name }}"
        state: present
```

#In this example, we define a task to install [Docker Compose](poe://www.poe.com/_api/key_phrase?phrase=Docker%20Compose&prompt=Tell%20me%20more%20about%20Docker%20Compose.), >

#Note that you should replace the variables `project_name` and `project_path` with the appropriate values for your project.

#Create a new file named hosts in the same directory as your playbook:
touch hosts

#Open the hosts file in a text editor and define the hosts for your playbook. Here is an example:
[my_servers]
server1 ansible_host=192.168.1.100
server2 ansible_host=192.168.1.101
#In this example, we define two hosts with their IP addresses.

#Create a new directory named files in the same directory as your playbook:
mkdir files

#Copy your Docker Compose file to the files directory:
cp docker-compose.yml files/

#Run the playbook using the following command:
ansible-playbook -i hosts my_playbook.yml


#This will run the tasks defined in your playbook and deploy your Docker Compose project on the hosts defined in your hosts file.

#Note that you should replace my_playbook.yml with the name of your playbook file, and hosts with the name of your hosts file if you named them differently.



