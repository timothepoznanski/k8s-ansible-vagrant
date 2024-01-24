# Kubernetes Cluster Setup with Ansible and Vagrant

Ce d�p�t fournit une configuration simple pour un cluster Kubernetes utilisant Ansible et Vagrant. Il vous permet de lancer rapidement un cluster Kubernetes multi-n�uds � des fins de d�veloppement et de test.

## Pr�requis

Avant de commencer, assurez-vous d'avoir install� les pr�requis suivants sur votre machine :

- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/)

## D�marrage rapide

1. **Initialisation de l'environnement Vagrant** :
    Ouvrez un terminal PowerShell et ex�cutez :

    ```powershell
    vagrant up
    ```

2. **Connexion SSH � l'administrateur** :
    Toujours dans PowerShell, connectez-vous au n�ud admin :

    ```powershell
    vagrant ssh admin
    ```

    Ensuite, passez � l'utilisateur admin :

    ```bash
    sudo su - adminuser
    ```

3. **Clonage du d�p�t et pr�paration** :
    Clonez le d�p�t et acc�dez au r�pertoire du projet :

    ```bash
    git clone https://github.com/timothepoznanski/k8s-ansible-vagrant.git
    cd k8s-ansible-vagrant/
    ```

4. **Ex�cution du playbook Ansible** :
    Lancez le playbook Ansible pour configurer le cluster Kubernetes :

    ```bash
    ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i inventory -u adminuser roles/main.yaml
    ```

5. **Connexion SSH au n�ud master** :
    Retournez � PowerShell pour vous connecter au n�ud master :

    ```powershell
    vagrant ssh master
    ```

    Passez ensuite � l'utilisateur admin :

    ```bash
    sudo su - adminuser
    ```

6. **V�rification des n�uds du cluster** :
    V�rifiez l'�tat des n�uds dans votre cluster Kubernetes :

    ```bash
    kubectl get nodes -o wide
    ```

    Vous devriez voir une sortie semblable � :

    ```
    NAME       STATUS   ROLES           AGE     VERSION   INTERNAL-IP     EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
    master     Ready    control-plane   5m24s   v1.28.2   192.168.50.11   <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.6.27
    worker-1   Ready    <none>          69s     v1.28.2   192.168.50.12   <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.6.27
    worker-2   Ready    <none>          69s     v1.28.2   192.168.50.13   <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.6.27
    ```

## Contribution

N'h�sitez pas � contribuer en ouvrant des issues ou des pull requests. Vos retours et contributions sont grandement appr�ci�s !


