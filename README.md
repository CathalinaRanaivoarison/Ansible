# Rôle Ansible : Webapp Apache Docker

## But du Projet
L'objectif de ce projet est de créer un rôle Ansible permettant de déployer automatiquement un serveur Apache dans un conteneur Docker sur une machine cliente CentOS 7. Ce rôle a été conçu pour être réutilisable, facilement configurable et adaptable à différentes situations, tout en assurant une installation rapide et fiable.

## Prérequis
- Ansible installé sur une machine de contrôle.
- Une machine cliente exécutant CentOS 7.
- Connexion SSH fonctionnelle entre la machine de contrôle et la cliente (de préférence avec une clé SSH).

## Configuration de l’Environnement
Suivez les étapes ci-dessous pour préparer votre environnement :

### 1. Création de l’environnement
- **Mettre en place un cluster** avec :
  - Une machine Ansible qui servira de poste d’administration.
  - Une machine cliente qui recevra les déploiements.
- **Configurer la connexion SSH sans mot de passe** entre Ansible et le client :
  ```bash
  ssh-keygen -t rsa
  ssh-copy-id user@client-ip
  ```
- **Vérifier les versions** sur les deux machines :
  ```bash
  cat /etc/centos-release
  ansible --version
  ```

### 2. Installation d’Ansible (si nécessaire)
Sur la machine de contrôle :
```bash
yum install epel-release -y
yum install ansible -y
```

### 3. Configuration de l’inventaire Ansible
Créez un fichier `inventory` avec le contenu suivant :
```
[client]
client-ip ansible_user=user
```

## Installation du Rôle
Clonez ce dépôt dans votre répertoire des rôles Ansible :

```bash
ansible-galaxy install git+https://github.com/votre-nom-utilisateur/ansible-role-webapp-apache-docker.git
```

## Variables
Vous pouvez personnaliser le déploiement en modifiant les variables suivantes :

| Variable                | Description                                      | Valeur par défaut   |
|-------------------------|--------------------------------------------------|---------------------|
| `docker_httpd_image`    | Image Docker d'Apache (depuis Docker Hub)         | `httpd:latest`      |
| `apache_container_name` | Nom du conteneur Apache                           | `webapp_apache`     |
| `apache_port`           | Port exposé sur l'hôte                            | `80`               |

## Exemple de Playbook
Voici un exemple minimal de playbook utilisant ce rôle :

```yaml
- name: Déployer Apache avec Docker
  hosts: client
  roles:
    - webapp_apache_docker
```

## Test du Rôle
Un playbook de test est fourni dans le dossier `tests/`. Vous pouvez l'exécuter avec :

```bash
ansible-playbook tests/test.yml -i inventory
```

## Vérification
Après le déploiement, vérifiez que le conteneur Apache est en cours d'exécution :

```bash
docker ps
```
Accédez au serveur Apache via votre navigateur :

```
http://<adresse-ip-client>:80
```

## Publication sur GitHub
Pour publier ce rôle sur GitHub :

```bash
git init
git remote add origin https://github.com/votre-nom-utilisateur/ansible-role-webapp-apache-docker.git
git add .
git commit -m "Initial commit"
git push origin main
```



