# ADR 0002: Estratégia de Exposição e Roteamento de Tráfego de Entrada

- **Status:** Aprovado
- **Data:** 2026-08-14

## Contexto
O tráfego de usuários precisa alcançar a API dentro do cluster Kubernetes de forma segura, com terminação TLS/SSL e suporte a múltiplos endpoints futuros sem a necessidade de alocar um endereço IP público caro para cada serviço.

## Decisão
Utilizar a combinação de um Cloud Load Balancer gerenciado na borda integrado a um Ingress Controller Nginx interno no cluster.

## Consequências
- **Positivas:**
  - Ponto centralizado para terminação TLS e aplicação de certificados.
  - Roteamento inteligente baseado em caminhos (/api, /docs) e hosts com um único IP público.
  - Economia de recursos de rede em nuvem.
- **Negativas:**
  - Camada adicional de rede (hop) entre o Load Balancer e o Pod da aplicação.
  - Exige manutenção e monitoramento das configurações do Ingress Controller.
