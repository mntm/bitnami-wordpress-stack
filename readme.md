# docker compose stack for wordpress
Huge shoutout to [Bitnami](https://github.com/bitnami) to give us access to powerful, headache-free config, and secure docker images.

## File structure

```
.
├── .dockerignore -> declares files that would be ignored by docker    
├── .env -> declares environment variables used by docker compose                               
├── .gitignore -> declares files that would be ignored by git
├── docker-compose.yml -> docker compose configuration file
├── host -> configuration files for the machine that runs docker (the host)
│   └── nginx
│       └── default.conf
└── readme.md -> this file
```

## Services

The stack consists of two services:
1. `mariadb`: mysql server
2. `wordpress`: wordpress server with php-fpm enabled

These services (containers) communicate with each other inside their own network: `wp_bitnami_network`.
The name of the services are important because docker compose will use them as hostname
for each container.

### Configuration

#### mariadb
Bitnami hardened MariaDB [image](https://hub.docker.com/r/bitnami/mariadb)

#### wordpress
Bitnami hardened Wordpress [image](https://hub.docker.com/r/bitnami/wordpress)

#### .env
Environment variables used by docker compose. To see all environment variables available: 
- mariadb: [Customizable environment variables](https://github.com/bitnami/containers/tree/main/bitnami/mariadb#customizable-environment-variables)
- wordpress: [Customizable environment variables](https://github.com/bitnami/containers/blob/main/bitnami/wordpress/README.md#customizable-environment-variables)

Check [`.env-example`](./.env-example) to have an idea of which env var is used in
this project.

### TODO
#### 1. Environment variables
Copy [`.env-example`](./.env-example) to .env and fill the variables approprietly

#### 2. Host nginx server
This part is only necessary if WP is hosted behind an nginx proxy
* Edit nginx [configuration](./host/nginx/default.conf). Replace `<domain>` by your domain name.
* Add your domain name to `/etc/hosts`, e.g: 127.0.0.1 `<domain>`
* Copy the nginx [configuration](./host/nginx/default.conf) to the `/etc/nginx/conf.d` (or where ever the nginx configuration lives)

