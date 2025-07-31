# DevOps Internship Task – Todo List Node.js
   ## Project Overview

This project is my submission for the DevOps Internship Task.
It demonstrates my skills in Docker, GitHub Actions (CI/CD), Ansible, Docker Compose, and an attempted Kubernetes deployment as a bonus.

The original repository for the Node.js Todo List app can be found here:
https://github.com/Ankit6098/Todo-List-nodejs



## Part 1: Docker + GitHub Actions CI
* Cloned the repository in VS Code.
* Configured .env to connect to my own MongoDB instance.
* Created a Dockerfile to containerize the Node.js Todo app.
* Implemented a GitHub Actions CI pipeline to:
  - Build the Docker image
  - Push it to my private Docker Hub registry
* Key Files:
  - Dockerfile
  - .github/workflows/ci.yml
* Proof:
  <img width="1482" height="446" alt="image" src="https://github.com/user-attachments/assets/e220d3cd-ad05-4a50-a979-514a15872cf2" />

  <img width="1830" height="892" alt="image" src="https://github.com/user-attachments/assets/2dd9fc02-3969-46d2-bb18-c69ee6833148" />

  
## Part 2: Linux VM + Ansible
For Part 2, I created a Linux virtual machine on the Azure cloud platform and used Ansible from my local machine to automate the configuration of the VM.
### Steps I Followed
+ Created a Linux VM on  Azure :
  - Launched an Ubuntu VM on Azure with a public IP address and SSH access enabled.
  - Copied the VM’s IP address to use in my Ansible inventory.
* Created Ansible Inventory :
  - Defined the VM in `hosts.ini`
* Wrote Ansible Playbook to Install Docker:
  - Created `install_docker.yml` to install Docker and required packages
* Executed the Playbook
 - ` ansible-playbook -i hosts.ini install_docker.yml `
   <img width="1223" height="608" alt="image" src="https://github.com/user-attachments/assets/372c708d-aae6-4b29-8224-368a69dae3e3" />

* Verified Docker Installation
  - ` docker --version `
  - ` systemctl status docker `
  - <img width="546" height="47" alt="image" src="https://github.com/user-attachments/assets/ab5db021-c76a-4ff6-a963-2a565314e380" />


## Part 3: Docker Compose + Auto Update
For Part 3, I deployed the application on the Azure VM using Docker Compose.
 ### Steps I Followed
* Created docker-compose.yml
  - Defined the Node.js Todo App service using the image from my private Docker Hub.
  - Added environment variables from the .env file to connect to my MongoDB instance.
  -  Configured health checks to ensure the container is running correctly.
* Started the Application
 - ` docker-compose up -d `
 - Verified the application is running successfully on the VM:
   ` docker ps `
 - Accessed the application through http://48.209.9.145:4000/

* Implemented Auto-Update
  - Used Watchtower to automatically pull new images and restart the container when a new version is pushed to Docker Hub.
  - Watchtower continuously monitors the running containers and the registry for updates.

* Key Files
- docker-compose.yml
- .env file (contains MongoDB URI )
- 
 <img width="1857" height="193" alt="image" src="https://github.com/user-attachments/assets/af5505f5-f91c-4015-bbf6-d7f202028966" />

## Bonus Part: Kubernetes Attempt
For the bonus part, I attempted to deploy the application on Kubernetes using Minikube.
### Steps I Followed
 * Installed Minikube and kubectl on the Azure VM.
* Started a local Kubernetes cluster using Minikube:

- `minikube start `
- ` kubectl get nodes `

- <img width="1256" height="447" alt="image" src="https://github.com/user-attachments/assets/5b691de2-507c-4a0f-a0d5-00f88100b00b" />

* Created a Kubernetes Secret to store the MongoDB URI securely
* Applied Kubernetes Deployment for the Node.js app:
  
* Verified the pods with:
  - ` kubectl get pods `
  - <img width="740" height="92" alt="image" src="https://github.com/user-attachments/assets/e11db340-08e9-4956-85dd-58b4c1782237" />

    
### Issue Faced
- The pods were created but the application did not start successfully.

- This was likely due to a configuration or connection bug with the MongoDB URI or ports.

 - I did not have enough time to fully debug and fix the issue before the deadline.
    
## Assumptions & Notes
* I used Watchtower for image auto-updates because it is lightweight and widely used in production for automated container restarts.

* No secrets are pushed to the repository.

* All configurations are tested in a Linux environment.


