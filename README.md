# next.js-deploy

Ce projet décrit comment déployer une application Next.js en utilisant Docker et Nginx Proxy Manager. 

Il est en lien avec les vidéos Youtube :

[Version Fast ⚡](youtu.be/sCzHpMbZ8Go)

[Version Longue 🐢](youtu.be/68x-eVevEG4)


## Prérequis

Avant de commencer, assurez-vous d'avoir installé Docker et Docker Compose sur votre machine. Vous pouvez suivre les instructions officielles pour installer Docker sur Ubuntu ici :

[Installer Docker sur Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

## Documentation

- [Documentation Next.js sur le déploiement](https://nextjs.org/docs/app/building-your-application/deploying)
- [Documentation Nginx Proxy Manager](https://nginxproxymanager.com/setup/)

## Étapes de déploiement

### 1. Créer un réseau Docker pour Nginx

Cette commande crée un réseau Docker nommé `nginx` qui sera utilisé pour connecter les conteneurs.

```sh
sudo docker network create nginx
```

### 2. Construire l'image Docker pour l'application Next.js

Utilisez la commande suivante pour construire l'image Docker à partir du Dockerfile dans le répertoire courant. L'option `-t nextjs-docker` attribue un nom à l'image Docker.

```sh
docker build -t nextjs-docker .
```

### 3. Démarrer les services avec Docker Compose

Cette commande démarre les services définis dans le fichier `docker-compose.yml` en mode détaché (en arrière-plan).

```sh
sudo docker compose up -d
```

### 4. Recréer les services avec Docker Compose

Si vous avez besoin de recréer les conteneurs (par exemple, après avoir modifié la configuration), utilisez l'option `--force-recreate`.

```sh
sudo docker compose up -d --force-recreate
```

### 5. Accéder au conteneur Nginx Proxy Manager

Pour accéder à un conteneur spécifique, utilisez `docker exec` avec l'option `-it` pour ouvrir une session interactive dans le conteneur `nginx-proxy-manager-app-1`.

```sh
sudo docker exec -it nginx-proxy-manager-app-1 bash
```

## Configuration Nginx Static HTML Export

Ajoutez la configuration suivante pour définir l'emplacement du site. Cette configuration indique à Nginx de servir le contenu du répertoire `/site/app-3` à la racine de l'URL.

```nginx
location / {
  root /site/app-3;
}
```

## Notes supplémentaires

- Assurez-vous de remplacer `/site/app-3` par le chemin correct vers le répertoire où votre application est déployée.
- Vérifiez les noms de conteneurs et les configurations spécifiques à votre environnement de déploiement.

## Conclusion

En suivant ces étapes, vous devriez être en mesure de déployer votre application Next.js en utilisant Docker et Nginx Proxy Manager. N'hésitez pas à consulter la documentation liée pour plus de détails et de configuration avancée.