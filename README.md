# Introdução

Pipeline de exemplo usando jenkins para a faculdade

# Passo 1

Buildar o dockerfile, que estava disponivel nas documentações do Jenkins

```bash
docker build -t myjenkins-blueocean:2.492.2-1 .
```

# Passo 2

Iniciar um comando a partir da imagem gerada:

```bash
docker run --name jenkins-blueocean --restart=on-failure --detach ^
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 ^
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 ^
  --volume jenkins-data:/var/jenkins_home ^
  --volume jenkins-docker-certs:/certs/client:ro ^
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.492.2-1
```

# Passo 3

Obtenha a senha inicial e forneça-a em http://localhost:8080/ para que o Jenkins possa iniciar suas configurações:

```bash
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
```

# Passo 4 

Após isso seu jenkins está configurado localmente. E Você pode começar a configurar suas pipelines para os projetos pertinentes.
