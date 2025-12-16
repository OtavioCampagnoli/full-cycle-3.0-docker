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