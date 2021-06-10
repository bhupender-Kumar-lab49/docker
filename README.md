#This section covers setting up private registry 

Pre - validation 
I hope you already have docker-destop installed on your windows machine or docker on Mac or linux 

Reason : Docker allows to setup private repository in your machine as well. So from CI/CD pipeline we can configure the private repo to pull image and execute 

Pre - requisite 
1) you should have certifactes as docker does not allow to have authentication without TCP 

If not we can generate with the below steps 
mkdir -p /certificates or mkdir  /certificates 
cd certificates
openssl req   -newkey rsa:4096 -nodes -sha256 -keyout domain.key   -x509 -days 365 -out domain.crt
#Enter all required fields 



Steps : 

1) Execute 
2) docker run -d -p 4000:5000 --restart=always --name registry -v /auth:/auth -e "REGISTRY_AUTH=htpasswd" -e "REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm"  -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd -v /certs:/certs -e REGISTRY_HTTP_TLS_CERTIFICATE=/certs/domain.crt   -e REGISTRY_HTTP_TLS_KEY=/certs/domain.key registry:2
3) Please change folder location as per your machine
4) you should have docker repository running 
5) docker ps 
6) you can stop with docker stop registry & docker rm registry 
7) docker pull hello-world
8) docker tag hello-world localhost:5000/hello-world
9) docker push localhost:5000/hello-world(this will not work)
10) docker login localhost:5000
11) to create user and password use 
12) docker run --rm --entrypoint htpasswd httpd:2 -Bbn testuser testpassword | Set-Content -Encoding ASCII auth/htpasswd
13) docker login localhost:5000
14) username:testuser
15) password:testpassword 
16) Done !!! 
