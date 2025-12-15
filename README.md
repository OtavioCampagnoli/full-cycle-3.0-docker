# Criando a primeira imagem com Dockerfile

- O objetivo é criar uma imagem personalizada, incluindo apenas os recursos necessários, e publicá-la no Docker Hub para facilitar o compartilhamento e reutilização.
- Principais comandos:
    - `docker build -t otaviocampagnoli/nginix-com-vim:latest .`: Cria a imagem Docker com a tag especificada.
    - `docker run -it otaviocampagnoli/nginix-com-vim:latest bash`: Executa um container interativo usando a imagem criada.
