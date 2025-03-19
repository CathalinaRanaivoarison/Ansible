# Rôle Ansible : Webapp Apache Docker

## Description
Ce rôle Ansible déploie Apache (en utilisant l'image Docker `httpd`) sur une machine cliente CentOS 7. Il installe les prérequis, configure Docker et lance un conteneur Apache prêt à servir un site web.

## Prérequis
- Ansible installé sur une machine de contrôle.
- Une machine cliente exécutant CentOS 7.
- Connexion SSH fonctionnelle entre la machine de contrôle et la cliente (de préférence avec une clé SSH).

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
git remote a
