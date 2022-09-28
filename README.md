# Introdução
O Portainer é um gerenciador amigável de containers, através ele podemos criar ambientes, configurar imagens e containers e muito mais em um navegador web.

# Sobre o portainer
O Portainer consiste em dois elementos: o servidor Portainer e o cliente. Ambos rodam como containers no seu Docker.
![Portainer Archtecture](https://github.com/witcliff-byte/docker-technologies/blob/main/images/portainer-architecture-detailed.png)
Um único Servidor Portainer irá aceitar conexões de vários clientes, habilitando a gerenciar multiplos clusters de uma única interface centralizada. Para isso, o container do servidor Portainer requer um volume de data persistente. O cliente portainer é indepentente,e os dados retornam para o container do servidor Portainer.

## Segurança e Certificação
O Portainer roda exclusivamente no seu servidor, com a sua rede, atrás do seu próprio firewall. Como resultado, o Portainer não usa nenhuma certificação SOC ou PCI/DSS porque não hospeda a infraestrutura do seu servidor. Você pode inclusive utilizar o Portainer completamente disconectado sem impactar em nada sua funcionalidade.

# Instalando o Portainer no Docker
1. Verifique por atualizações de sistema com `sudo apt update`
2. Antes de instalarmos o Portainer, precisamos criar um volume, que irá armazenar de forma persistente os dados do Portainer, com `docker create volume portainer_data`
3. Após isso, devemos rodar o comando`docker run -d -p 9443:9443 -p 8000:8000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest` nós estaremos expondo as portas `9443` e `8000`, depois em `-v /var/run/docker.sock:/var/run/docker.sock` estaremos mapeando algumas coisas específicas do Docker para o conteiner, para que você possa acessar o seu próprio ambiente local pelo Portainer, e com `-v portainer_data:/data` estamos mapeando o volume que criamos para os dados do portainer permanecerem.
4. Verifique se seu container está funcionando com `docker ps`
5. Entre no seu endereço de IP por um navegador web, especificando a porta que expomos com protocolo https: `https://meu_ip_addr:9443`
6. Crie uma senha para seu usuário administrador.
![Portainer Painel](https://github.com/witcliff-byte/docker-technologies/blob/main/images/portaineradm.png)
## Ambientes
![Portainer Env](https://github.com/witcliff-byte/docker-technologies/blob/main/images/portainerenv.png)
## Dashboard
![Portainer Dashboard](https://github.com/witcliff-byte/docker-technologies/blob/main/images/portainerdash.png)
# Referências
[Documentação Oficial](https://docs.portainer.io/start/architecture)

[learning Docker is HARD!! ~ Network Chuck](https://www.youtube.com/watch?v=iX0HbrfRyvc&t=85s)
