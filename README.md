# next.js-deploy

This project describes how to deploy a Next.js application using Docker and Nginx Proxy Manager.

It is linked to the following YouTube videos:

[Fast Version ⚡](youtu.be/sCzHpMbZ8Go)

[Long Version 🐢](youtu.be/68x-eVevEG4)

[Readme fr 🇫🇷](https://github.com/fab-uleuh/next.js-deploy/blob/main/README.md)

## Prerequisites

Before starting, make sure you have Docker and Docker Compose installed on your machine. You can follow the official instructions to install Docker on Ubuntu here:

[Install Docker on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

## Documentation

- [Next.js Deployment Documentation](https://nextjs.org/docs/app/building-your-application/deploying)
- [Nginx Proxy Manager Documentation](https://nginxproxymanager.com/setup/)

## Deployment Steps

### 1. Create a Docker Network for Nginx

This command creates a Docker network named `nginx` that will be used to connect the containers.

```sh
sudo docker network create nginx
```

### 2. Build the Docker Image for the Next.js Application

Use the following command to build the Docker image from the Dockerfile in the current directory. The `-t nextjs-docker` option assigns a name to the Docker image.

```sh
docker build -t nextjs-docker .
```

### 3. Start the Services with Docker Compose

This command starts the services defined in the `docker-compose.yml` file in detached mode (in the background).

```sh
sudo docker compose up -d
```

### 4. Recreate the Services with Docker Compose

If you need to recreate the containers (e.g., after modifying the configuration), use the `--force-recreate` option.

```sh
sudo docker compose up -d --force-recreate
```

### 5. Access the Nginx Proxy Manager Container

To access a specific container, use `docker exec` with the `-it` option to open an interactive session in the `nginx-proxy-manager-app-1` container.

```sh
sudo docker exec -it nginx-proxy-manager-app-1 bash
```

## Nginx Static HTML Export Configuration

Add the following configuration to define the site location. This configuration tells Nginx to serve the content from the `/site/app-3` directory at the root of the URL.

```nginx
location / {
  root /site/app-3;
}
```

## Additional Notes

- Make sure to replace `/site/app-3` with the correct path to the directory where your application is deployed.
- Check the container names and configurations specific to your deployment environment.

## Conclusion

By following these steps, you should be able to deploy your Next.js application using Docker and Nginx Proxy Manager. Feel free to consult the linked documentation for more details and advanced configuration.