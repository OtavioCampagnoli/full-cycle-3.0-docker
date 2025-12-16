# Trabalhando com Imagens - Criando a primeira imagem com Dockerfile

- O objetivo é criar uma imagem personalizada, incluindo apenas os recursos necessários, e publicá-la no Docker Hub para facilitar o compartilhamento e reutilização.
- Principais comandos:
    - `docker build -t otaviocampagnoli/nginix-com-vim:latest .`: Cria a imagem Docker com a tag especificada.
    - `docker run -it otaviocampagnoli/nginix-com-vim:latest bash`: Executa um container interativo usando a imagem criada.

# Trabalhando com Imagens - Avançando com Dockerfile

- O obejtivo é criar um diretorio usando o comando `WORKDIR` e copiar a pasta que foi refletida por outro container usando o comando: `docker run -d -p 8080:80 --name ngnix-volume-demo --mount type=bind,source=/home/otavio/FullCycle/full-cycle-3.0-docker/html,target=/usr/share/nginx/html`
- Buildar a imagem novamente e verificar que cada etapa foi realizada e que cada etapa tem um chuck que é gerado e cache onde a aquele nova versão da imagem não precisa compilar aquela etapa novamente.

# Trabalhando com Imagens - ENTRYPOINT vs CMD


## Diferença entre CMD e ENTRYPOINT (para crianças!)

Imaginem que vocês estão construindo um robô! 🤖

### ENTRYPOINT: O que o robô SEMPRE faz!

Pensem no `ENTRYPOINT` como a **ação principal** que o seu robô foi feito para fazer. É como se ele sempre tivesse um "trabalho" fixo.

Se o seu robô é um "robô de saudar", o `ENTRYPOINT` dele pode ser "dizer". Ele **sempre vai dizer alguma coisa**.

### CMD: O que o robô faz por padrão, mas pode mudar!

Agora, o `CMD` é o que o robô **diz por padrão** se ninguém falar nada. Se o robô de saudar não receber nenhuma instrução, ele pode dizer "Olá!".

Mas se você disser para ele "dizer Tchau!", ele vai mudar o que diz. O `CMD` é como a "palavra padrão" que ele usa, mas você pode dar uma palavra diferente para ele usar no lugar.

### Juntos, eles trabalham assim:

Se o `ENTRYPOINT` é "dizer" e o `CMD` é "Olá!", o robô vai "dizer Olá!".

Mas se você disser para o robô "dizer Tchau!", ele vai "dizer Tchau!" e vai ignorar o "Olá!" do `CMD`.

No nosso Dockerfile, o robô (nosso container) **sempre vai "echo" (falar)** o que vem depois do `ENTRYPOINT`. E por padrão, ele vai "falar" "Mundo!" (que é o `CMD`).

Então, ele vai "falar Olá, Mundo!".

Mas se você rodar o container e disser para ele "falar Sol!", ele vai "falar Olá, Sol!". Ele sempre usa o "Olá," do `ENTRYPOINT` e junta com o que você manda ou com o `CMD` padrão.

# Trabalhando com Imagens - Docker entrypoint exec

- O ENTRYPOINT define o comando principal da imagem.
- O CMD define o comando padrão, que pode ser sobrescrito ao rodar o container.
- Se passar um comando ao iniciar o container (ex: bash), ele substitui o CMD.
```dockerfile
    # Exemplo de Dockerfile
    FROM ubuntu:latest

    ENTRYPOINT ["echo", "Olá,"]
    CMD ["Mundo!"]
```

# Trabalhando com Imagens - Publicando Imagem no DockerHub

- **Listar todos os containers:**  
  `docker ps -a`

- **Rodar um container em background:**  
  `docker run -d --name ocampagnoli-fullcycle-nginx -p 8080:80 ocampagnoli/full-cycle-nginx:latest`

- **Listar containers em execução:**  
  `docker ps`

- **Listar todas as imagens:**  
  `docker images -a`  
  ou  
  `docker images`

- **Filtrar imagens por status:**  
  `docker images --filter status=exited`

- **Publicar imagem no DockerHub:**  
  `docker push ocampagnoli/full-cycle-nginx:latest`

- **Criar imagem a partir do Dockerfile:**  
  `docker build -t ocampagnoli/full-cycle-nginx .`

- **Remover containers parados:**  
  `docker rm -f $(docker ps -a -f status=exited -q)`