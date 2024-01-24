# Kubernetes Cluster Setup with Ansible and Vagrant

Ce dépôt fournit une configuration simple pour un cluster Kubernetes utilisant Ansible et Vagrant. Il vous permet de lancer rapidement un cluster Kubernetes multi-nœuds à des fins de développement et de test.

## Prérequis

Avant de commencer, assurez-vous d'avoir installé les prérequis suivants sur votre machine :

- [Vagrant](https://www.vagrantup.com/)
- [VirtualBox](https://www.virtualbox.org/)

## Démarrage rapide

1. **Initialisation de l'environnement Vagrant** :
    Ouvrez un terminal PowerShell et exécutez :

    ```powershell
    vagrant up
    ```

2. **Connexion SSH à l'administrateur** :
    Toujours dans PowerShell, connectez-vous au nœud admin :

    ```powershell
    vagrant ssh admin
    ```

    Ensuite, passez à l'utilisateur admin :

    ```bash
    sudo su - adminuser
    ```

3. **Clonage du dépôt et préparation** :
    Clonez le dépôt et accédez au répertoire du projet :

    ```bash
    git clone https://github.com/timothepoznanski/k8s-ansible-vagrant.git
    cd k8s-ansible-vagrant/
    ```

4. **Exécution du playbook Ansible** :
    Lancez le playbook Ansible pour configurer le cluster Kubernetes :

    ```bash
    ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i inventory -u adminuser roles/main.yaml
    ```

5. **Connexion SSH au nœud master** :
    Retournez à PowerShell pour vous connecter au nœud master :

    ```powershell
    vagrant ssh master
    ```

    Passez ensuite à l'utilisateur admin :

    ```bash
    sudo su - adminuser
    ```

6. **Vérification des nœuds du cluster** :
    Vérifiez l'état des nœuds dans votre cluster Kubernetes :

    ```bash
    kubectl get nodes -o wide
    ```

    Vous devriez voir une sortie semblable à :

    ```
    NAME       STATUS   ROLES           AGE     VERSION   INTERNAL-IP     EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
    master     Ready    control-plane   5m24s   v1.28.2   192.168.50.11   <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.6.27
    worker-1   Ready    <none>          69s     v1.28.2   192.168.50.12   <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.6.27
    worker-2   Ready    <none>          69s     v1.28.2   192.168.50.13   <none>        Ubuntu 22.04.3 LTS   5.15.0-91-generic   containerd://1.6.27
    ```

## Contribution

N'hésitez pas à contribuer en ouvrant des issues ou des pull requests. Vos retours et contributions sont grandement appréciés !


