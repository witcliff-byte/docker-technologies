# Introdução: #

* É possível, através do Docker Compose rodar facilmente o Wordpress em um ambiente isolado construido com Docker Containers. Esse pequeno passo a passo mostra como configurar e executar o Wordpress com o Docker Compose. Antes de iniciar, certifique-se de ter instalado o Docker e Docker Compose no seu sistema. 
** Este tutorial não tem por fim explicar como instalar essas ferramentas,mas aqui estão os links da documentação oficial para instalar tanto o [Docker](https://docs.docker.com/engine/install/ubuntu/) quanto o [Docker-compose](https://docs.docker.com/compose/install/) 
### Passo 1: ###
* Crie um diretório de projeto vazio.
* Você pode nomear o diretório com um nome que vá se lembrar facilmente do que se trata em outros momentos, o nome do diretório portanto, fica a seu critério.
`mkdir diretorio-compose`
Este projeto vai conter o `docker-compose.yml` que iniciará o Wordpress em ambiente isolado.
### Passo 2:
* Mude para o diretório criado:
`cd diretorio-compose`
### Passo 3:
* Crie o arquivo docker-compose.yml, que irá iniciar o Wordpress e separar o MySQL com montagem de volume para a persistencia de dados:
```version: "3.9"
    
services:
  db:
    image: mysql:5.7
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: somewordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress
    
  wordpress:
    depends_on:
      - db
    image: wordpress:latest
    volumes:
      - wordpress_data:/var/www/html
    ports:
      - "8000:80"
    restart: always
    environment:
      WORDPRESS_DB_HOST: db:3306
      WORDPRESS_DB_USER: wordpress
      WORDPRESS_DB_PASSWORD: wordpress
      WORDPRESS_DB_NAME: wordpress
volumes:
  db_data: {}
  wordpress_data: {}
```
## Criando o Projeto

* Rode `docker-compose up -d`
** Esse comando em detached mode, ira baixar todas as imagens Docker necessárias,e irá iniciar o wordpress e os containers de banco de dados.
Testando

* Para verificar se está funcionando, acesse no seu navegador `http://localhost:8000` e inicie a configuração do seu Wordpress.
## Desligando e Limpando

* O comando `docker-compose down` remove os containers e as networks padrão, mas mantém o banco de dados do seu Wordpress.
* O Comando `docker-compose down --volumes` remove os containers, as networks padrão e os bancos de dados
## Referências: [Compose and Wordpress](https://docs.docker.com/samples/wordpress/)
