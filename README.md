# Imagens Bitnami

Durante 18 anos, as [Imagens Bitnami](https://github.com/bitnami/containers) eram livres para uso sem requerer subscrição/pagamento.

Iniciando em 28 de agosto de 2025, as maioria das imagens requerem subscrição com a justificativa:
* [Bitnami Secure Images Helps Keep Applications More Secure with Hardened Software Packages, Minimal CVEs, Support and Radical Transparency](https://news.broadcom.com/app-dev/broadcom-introduces-bitnami-secure-images-for-production-ready-containerized-applications)

Essa decisão afetou diversos usuários que antes utilizavam as Imagens de forma livre.

No caso do WordPress, as imagens **docker.io/bitnami/wordpress-nginx:latest** e **docker.io/bitnami/mariadb:latest** não estão mais disponíveis para serem utilizadas e nem receberão atualizações.
* Nem adianta abrir uma issue relatando o problema causado https://github.com/bitnami/containers/issues/86874

# Imagens Oficiais

* Como instanciar um WordPress do Zero em docker utilizando apenas imagens oficiais?

De acordo com https://br.wordpress.org/download/ (em 09/Out/2025) as recomendações são: PHP 8.3 ou superior, versão do MySQL 8.0 ou a versão do MariaDB 10.6 ou superior.

Então vamos utilizar as imagens abaixo:

* Banco de Dados: [mariadb:latest - versão 12](https://hub.docker.com/_/mariadb)
* WordPress: [wordpress:fpm - versão 6.8.3 ](https://hub.docker.com/_/wordpress)
* Servidor Web: [nginx:latest - versão 1.29.2](https://hub.docker.com/_/nginx) 
* Porquê Nginx ao invés do Apache?
  * Performance: - https://www.hostinger.com/br/tutoriais/nginx-vs-apache
  * Grandes sites: https://developer.wordpress.org/advanced-administration/server/web-server/nginx/

# Obtendo o código

* Basta um **git clone** básico:
```bash
git clone https://github.com/jarbelix/wordpress-nginx.git
cd wordpress-nginx
```
## Utilizando Certificados Digitais Auto-Assinados

Para o funcionamento seguro é fundamental que o tráfego entre o Browser e o Servidor Nginx seja criptografado.

Mesmo utilizando um **Self-Signed Certificate** não há como um **tcpdump** bisbilhoteiro **ler** o trafego.

## Gerando Certificados Auto-Assinados

Basta uma única linha de comando com o **openssl** para obter os arquivos de chave privada (**nginx.key**) e certificado (**nginx.crt**). Os arquivos nesse repositório foram gerados conforme abaixo:

```bash
openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout nginx.key -out nginx.crt -subj "/C=US/ST=State/L=City/O=Organization/CN=localhost"
```
* Fonte: https://ecostack.dev/posts/nginx-self-signed-https-docker-compose/


## Customizando com suas preferências

* O arquivo [docker-compose.yml](docker-compose.yml) pode ser editado para refretir suas preferências (portas expostas, versão das imagens, etc). Quando em produção, remova a entrada do volume **info.php** que serve apenas para validar se as variáveis PHP foram aplicadas corretamente

* O arquivo [custom-nginx.conf](custom-nginx.conf) contém as configurações básicas do servidor Nginx

* O arquivo [custom-php.ini](custom-php.ini) contém as configurações de variáveis do PHP

## Subir o Stak (mais de um container simultâneo)
```bash
docker compose up -d
```

# Instalando e Configurando seu Wordpress

Acesse https://localhost ou o FQDN (ex: https://wordpress.tiozaodolinux.com) do seu site.

Seguir as orientações conforme prints abaixo:

* Alerta de conexão insegura

![Tela-01](screenshots/Wordpress-Nginx-01.png)

* Aceitar os riscos

![Tela-02](screenshots/Wordpress-Nginx-02.png)

* Escolha do Idioma

![Tela-03](screenshots/Wordpress-Nginx-03.png)

* Preencher com suas informações

![Tela-04](screenshots/Wordpress-Nginx-04.png)

* Instalação concluída

![Tela-05](screenshots/Wordpress-Nginx-05.png)

* Login na Área Administrativa

![Tela-06](screenshots/Wordpress-Nginx-06.png)

* Visualiando o Conteúdo Inicial

![Tela-07](screenshots/Wordpress-Nginx-07.png)
