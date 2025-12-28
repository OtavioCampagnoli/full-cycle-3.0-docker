# Entendendo tipos de Network

- bridge: A rede padrão criada pelo Docker. Permite comunicação entre containers no mesmo host.
  - Exemplo: `docker run --network bridge my_image` (padrão)
- host: O container compartilha a rede do host, sem isolamento de rede.
  - Exemplo: `docker run --network host my_image`
- none: O container não tem rede.
  - Exemplo: `docker run --network none my_image`
- overlay: Permite comunicação entre containers em diferentes hosts Docker, usado em clusters.
  - Exemplo: `docker network create -d overlay my_overlay_network`
- macvlan: Permite atribuir um endereço MAC ao container, fazendo com que ele apareça como um dispositivo físico na rede.
  - Exemplo: `docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 my_macvlan_network`

# Trabalhando com bridge

## Exemplos práticos com bridge

- **Criar uma rede bridge personalizada:**

  ```bash
  docker network create --driver bridge minharede
  ```

- **Listar redes existentes:**

  ```bash
  docker network ls
  ```

- **Inspecionar detalhes de uma rede:**

  ```bash
  docker network inspect minharede
  ```

- **Adicionar um container à rede:**

  ```bash
  docker network connect minharede meu_container
  ```

- **Remover um container da rede:**

  ```bash
  docker network disconnect minharede meu_container
  ```

- **Remover uma rede:**

  ```bash
  docker network rm minharede
  ```

- **Iniciar um container já conectado à rede:**

  ```bash
  docker run -dit --name ubuntu1 --network minharede ubuntu
  ```

- **Verificar redes de um container:**

  ```bash
  docker inspect ubuntu1
  ```

- **Testar comunicação entre containers na mesma rede:**

  ```bash
  docker exec -it ubuntu1 ping ubuntu2
  ```

- **Consultar IP de um container:**
  ```bash
  docker exec -it meu_container ip addr show
  ```

# Trabalhando com host

## Exemplos práticos com host

- **Executar Nginx usando a rede do host:**
  ```bash
  docker run -d --name nginx -p 8080:80 --network host nginx
  ```
- **Acessar o serviço:**
  - Abra o navegador e acesse `http://localhost:8080` para ver a página padrão do Nginx.
- **Verificar a rede do container:**
  ```bash
  docker inspect nginx
  ```

# Container acessando nossa maquina

- **Executar um container com rede host:**
  ```bash
  docker run -dit --name meu_container --network host ubuntu
  ```
- **Dentro do container, acessar um serviço rodando na máquina host:**
  ```bash
  docker exec -it meu_container bash
  curl http://localhost:porta_do_servico
  ```
- **Exemplo prático:**
  - Se você tiver um servidor web rodando na sua máquina host na porta 4200, pode acessá-lo de dentro do container usando `curl http://localhost:4200` (quando estiver usando a rede `host`).
  - Caso esteja usando a rede padrão (`bridge`), utilize o hostname especial `host.docker.internal`, assim: `curl http://host.docker.internal:4200`. Esse hostname resolve para o IP da máquina host a partir de containers Docker (disponível nativamente no Docker Desktop e em algumas distribuições Linux recentes; em outras, pode ser necessário configuração adicional).
