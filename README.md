# Taiga Docker

This is a deployment based on taiga-docker ( https://github.com/taigaio/taiga-docker // Tag: 6.0.4 ) with LDAP-support.

It is deployed without exposing ports because it is intended to be deplyoed behind an SSL NGINX webserver.
It is also intended to make use of an existing mail-server & LDAP over TLS
The docker-compose-file also contains the configuration for binding the infrastructure to another docker networks containing the mailserver & the webserver.
If you dont want to make use of some properties, just remove them from `docker-compose.yml`.
The LDAP & email properties are commented out & you need to add them by yourself in `docker-compose.yml` & `.env`.

## Requirements
`Docker` & `docker-compose` are required.

## Getting started

Clone this repo and change into it
```sh
git clone https://gitlab.bjoern-freund.de/docker/taiga.git
cd taiga
```

### LDAP (optional)

If you want to make use of LDAP you need to add the LDAP-configuration to the Taiga-Backend.
In this deployment the taiga-back Docker-image is customized.
The build-process of the custom-image adds a small routine to the entrypoint-script which adds the LDAP-config during the initial container startup.

**Build taiga-bakend with LDAP**

```sh
cd ldap
docker build -t taiga-back .
cd ..

# Change the image-tag of taiga-back in docker-compose
sed -i 's/image: taigaio\/taiga-back:latest/image: taiga-back/g' docker-compose.yml
```

### Configuration

The whole configuration is done with adjusting`.env` & `docker-compose.yml`.
Just adjust it & replace the example values with your desired properties.

### Deployment
```
docker-compose up -d
```

# Enjoy!
