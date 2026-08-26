# 🌐 Nginx Load Balancer & Reverse Proxy Lab

## 🚀 Sobre o Projeto
Este repositório documenta a configuração de um ambiente de infraestrutura de alta disponibilidade utilizando máquinas virtuais. O objetivo principal foi criar um Balanceador de Carga (Load Balancer) com Nginx atuando como Proxy Reverso para isolar e distribuir o tráfego entre múltiplos servidores web. 


## 🏗️ Arquitetura de Rede
O laboratório foi estruturado com três instâncias do Ubuntu Server isoladas:

*   **Load Balancer (Ponto de Entrada):** Possui comunicação com o Host (via Host-Only) e encaminha as requisições na porta 80.
*   **Web Server 01 (Isolado):** Conectado apenas à rede interna (para receber o tráfego do balanceador) e ao NAT.
*   **Web Server 02 (Isolado):** Conectado apenas à rede interna e ao NAT.

**Fluxo da Requisição:** `Host (Mac)` ➔ `Rede Host-Only` ➔ `Load Balancer (Nginx)` ➔ `Rede Interna (Proxy Pass)` ➔ `Servidores Web`.

## 🛠️ Tecnologias Utilizadas
*   **Sistema Operacional:** Ubuntu Server 24.04 (Máquinas Virtuais clonadas).
*   **Servidor Web/Proxy:** Nginx.
*   **Redes:** Netplan (Configuração de interfaces via YAML).
*   **Ferramentas:** SSH, cURL, Git.

## 🧠 Principais Configurações e Desafios
Durante a implementação, as seguintes etapas foram realizadas:
*   **Clonagem Segura de VMs:** Geração de novos endereços MAC para evitar conflitos de rede entre as instâncias clonadas.
*   **Mapeamento de Interfaces (Netplan):** Correção de inconsistências no Ubuntu entre os nomes lógicos das placas (como `enp0s8` e `enp0s10`) e os endereços físicos (MAC Addresses) após a clonagem.
*   **Isolamento de Rede:** Remoção dos IPs de rede Host-Only dos servidores web locais, garantindo que o tráfego passe obrigatoriamente pela rede privada (`10.0.0.x`).
*   **Configuração de Proxy Reverso:** Implementação do bloco `upstream` no Nginx, utilizando o algoritmo padrão *Round-Robin* para distribuir as requisições alternadamente entre os nós de serviço.