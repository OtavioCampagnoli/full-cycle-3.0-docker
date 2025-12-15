# Trabalhando com Imagens - Criando a primeira imagem com Dockerfile

- O objetivo é criar uma imagem personalizada, incluindo apenas os recursos necessários, e publicá-la no Docker Hub para facilitar o compartilhamento e reutilização.
- Principais comandos:
    - `docker build -t otaviocampagnoli/nginix-com-vim:latest .`: Cria a imagem Docker com a tag especificada.
    - `docker run -it otaviocampagnoli/nginix-com-vim:latest bash`: Executa um container interativo usando a imagem criada.

# Trabalhando com Imagens - Avançando com Dockerfile

- O obejtivo é criar um diretorio usando o comando `WORKDIR` e copiar a pasta que foi refletida por outro container usando o comando: `docker run -d -p 8080:80 --name ngnix-volume-demo --mount type=bind,source=/home/otavio/FullCycle/full-cycle-3.0-docker/html,target=/usr/share/nginx/html`
- Buildar a imagem novamente e verificar que cada etapa foi realizada e que cada etapa tem um chuck que é gerado e cache onde a aquele nova versão da imagem não precisa compilar aquela etapa novamente.