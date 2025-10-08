# wordpress-nginx

Como instanciar um WordPress do Zero em docker utilizando apenas imagens oficiais


## Generate Self-Signed Certificate

* https://ecostack.dev/posts/nginx-self-signed-https-docker-compose/

```bash
openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout nginx.key -out nginx.crt -subj "/C=US/ST=State/L=City/O=Organization/CN=localhost"
```


## Clonar o repositório e subir os containers

git clone https://github.com/jarbelix/wordpress-nginx.git
cd wordpress-nginx
docker compose up -d

## Configurar seu Wordpress

Acesse https://seu-ip:8443

Informe:

Nome do Site: XXXXX
Usuário: XXXXX
Senha: XXXXX
Email: XXXXX


