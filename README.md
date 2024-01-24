# Kubernetes Cluster Setup with Ansible and Vagrant

This repository provides a straightforward configuration for a Kubernetes cluster using Ansible and Vagrant. It allows you to quickly launch a multi-node Kubernetes cluster for development and testing purposes.

## Prerequisites

Before you begin, ensure you have installed the following prerequisites on your machine:

- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/)
- Add your id_rsa and id_rsa.pub files to your ~/.ssh/ windows directory

## Quick Start

1. **Initializing the Vagrant Environment**:
   
    Open a PowerShell terminal and execute:

    ```powershell
    vagrant up
    ```

3. **SSH Connection to the Admin Node**:
   
    Still in PowerShell, connect to the admin node:

    ```powershell
    vagrant ssh admin
    ```

    Then, switch to the admin user:

    ```bash
    sudo su - adminuser
    ```

    Then, load your ssh private key in this powershell session.

5. **Cloning the Repository and Preparation**:
   
    Clone the repository and navigate to the project directory:

    ```bash
    git clone https://github.com/timothepoznanski/k8s-ansible-vagrant.git
    cd k8s-ansible-vagrant/
    ```

7. **Executing the Ansible Playbook**:
   
    Launch the Ansible playbook to set up the Kubernetes cluster:

    ```bash
    ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i inventory -u adminuser roles/main.yaml
    ```

9. **SSH Connection to the Master Node**:
    
    Return to PowerShell to connect to the master node:

    ```powershell
    vagrant ssh master
    ```

    Then, switch to the admin user:

    ```bash
    sudo su - adminuser
    ```

11. **Verifying the Cluster Nodes**:
    
    Check the status of the nodes in your Kubernetes cluster:

    ```bash
    kubectl get nodes -o wide
    ```

    You should see output similar to:

    ```
    NAME       STATUS   ROLES           AGE     VERSION   INTERNAL-IP     EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
    master     Ready    control-plane   5m24s   v1.28.2   192.168.50.11   <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.6.27
    worker-1   Ready    <none>          69s     v1.28.2   192.168.50.12   <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.6.27
    worker-2   Ready    <none>          69s     v1.28.2   192.168.50.13   <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.6.27
    ```

## Contributing

Feel free to contribute by opening issues or pull requests. Your feedback and contributions are greatly appreciated!
