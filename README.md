# Agroconect-loadbalancer

Load Balancer com Nginx contendo 5 nós e cada nó recebendo a identificação dos IPs de requisição

#### 1. Para criar os nós execute os comandos abaixo no terminal:
   
   ```sh
   docker run -it -v ./build:/usr/share/nginx/html -v ./nginx.conf:/etc/nginx/nginx.conf -v ./app.conf:/etc/nginx/conf.d/default.conf --name node1 nginx:alpine /bin/sh
   docker run -it -v ./build:/usr/share/nginx/html -v ./nginx.conf:/etc/nginx/nginx.conf -v ./app.conf:/etc/nginx/conf.d/default.conf --name node2 nginx:alpine /bin/sh
   docker run -it -v ./build:/usr/share/nginx/html -v ./nginx.conf:/etc/nginx/nginx.conf -v ./app.conf:/etc/nginx/conf.d/default.conf --name node3 nginx:alpine /bin/sh
   docker run -it -v ./build:/usr/share/nginx/html -v ./nginx.conf:/etc/nginx/nginx.conf -v ./app.conf:/etc/nginx/conf.d/default.conf --name node4 nginx:alpine /bin/sh
   docker run -it -v ./build:/usr/share/nginx/html -v ./nginx.conf:/etc/nginx/nginx.conf -v ./app.conf:/etc/nginx/conf.d/default.conf --name node5 nginx:alpine /bin/sh
   ```
   
#### 2. O comando acima abrirá o shell para cada nó criado. No shell de cada nó obtenha o ip e cole-o no arquivo default do projeto:
   
 ```nginx
     hostname -i
   ```
   
#### 3. Agora vamos criar o nosso balanceador. No terminal do projeto execute o comando abaixo:
   
  ```sh
    docker run -it -p 80:80 -v ./default.conf:/etc/nginx/conf.d/default.conf --name loadbalancer nginx:alpine
  ```
    
**Agora pode visualizar a aplicação disponível no localhost/**

#### 4. Para visualizar o ip do cliente, execute o comando abaixo no shell de cada nó:
   
  ```nginx
    tail -f /var/log/nginx/nginx-access.log
   ```
