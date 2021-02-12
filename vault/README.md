# Vault Docker Compose

* this docker-compose.yml file runs HashiCorp vault server in container

## Run vault without SSL 
* run the following command:
    ```bash
    docker-compose up -d
    ```
* go to http://localhost:8200 to unseal and use vault
* check https://learn.hashicorp.com/tutorials/vault/getting-started-ui?in=vault/getting-started on how to unseal and use vault server

## Run vault with SSL
* create self-signed certificate files:
    ```bash
    openssl req -newkey rsa:4096 \
                -x509 \
                -sha256 \
                -days 3650 \
                -nodes \
                -out vault.crt \
                -keyout vault.key
    ```
* copy your certificate files and replace the one under `./vault/config`
* modify the `docker-compose.yml` to use the `config_ssl.json`;
    ```
    command: vault server -config=/vault/config/config_ssl.json
    ```
* start container and go to https://localhost:8200
* **Note** if you started container, the `config` folder may need `sudo` to access afterwards

## Disable UI (more secure)
* delete the following line in `config.json` or `config_ssl.json`
    ```
    "ui": true
    ```


