Primeiro, se foi criado o DockerFile utilizando a imagem do MySql.

Depois, criei a imagem "mysql-image" com o comando:
   docker build -t mysql-image -f api/db/Dockerfile .

Depois de criar a imagem, criei o container, com o comando:
    docker run -d -v ${pwd}/api/db/data:/var/lib/mysql --rm --name mysql-container mysql-image

Após criar o container, executei o container utilizando o Mysql, com o comando: 
    Get-Content api/db/script.sql | docker exec -i mysql-container mysql -uroot -pprogramadorabordo

E utilizei a ferramenta bash com o seguinte comando:
    docker exec -it mysql-container-devops /bin/bash
E selecionei minha tabela no MYSQL. 

Volumes: 

Para criar um volume utilizei o seguinte comando: 
    docker run -d -v ${PWD}/api/db/data:/var/lib/mysql --rm --name  mysql-container mysql-image

Node:
Utilizando o node, foi-se criada uma api para ser utilizada, logo após baixei o nodemon e o express, utilizando os comandos: 
    npm install --save-dev nodemon
    npm install --save express mysql

Criação de rede:
Após instalar tudo, acrescentei no arquivo package.json o comando:
    "start": "nodemon ./src/index"

Logo após, criei uma pasta chamada src e um arquivo chamado index, no arquivo index, fiz as conexões com o host utilizando nodeJS.

Então criei uma imagem Node, e usei o comando: 
    docker build -t node-image -f api/Dockerfile .

Após isso fiz a criação de outro container para o node, e o coloquei na porta 9001, com o seguinte comando: 
    docker run -d -v ${PWD}/api:/home/node/app -p 9001:9001 --rm --name node-container node-image

Após isso, criei o arquivo php para rodar a aplicação, criei a imagem e o container dele na porta 8888:80, utilizando os comandos:
    docker build -t php-image -f website/Dockerfile .
    docker run -d -v ${pwd}/website:/var/www/html -p 8888:80 --link node-container --rm --name php-container php-image

Lembrando que foi utilizado o NODE 10, pois utilizei um tutorial como referência para fazer o desafio. 

Nome: Felipe Mateus Machado de Lima


