**Aluno:** Michelle Teles Soares
**Repositório do Projeto:** https://github.com/micknek/move-tech-cloud-application-comp-6

# Documentação de Arquitetura da Solução

## 1. Mapeamento de Recursos (Cluster & Cloud)
- **Cluster Kubernetes (K3s / Magalu Cloud):**
  - **App API:** Contêiner de aplicação backend (FastAPI / Python).
  - **Ingress Controller (Nginx):** Ponto de entrada de rede e roteamento interno HTTP/HTTPS.
  - **Observabilidade:** Agentes Prometheus (coleta de métricas) e Grafana (visualização).
- **Serviços Gerenciados / Externos (Magalu Cloud):**
  - **Banco de Dados Gerenciado (DBaaS):** Instância PostgreSQL gerenciada com backups e alta disponibilidade.
  - **Container Registry (MCR):** Armazenamento seguro de imagens Docker.
  - **Load Balancer (Cloud LB):** Balanceador de carga de entrada para tráfego externo.

## 2. Diagrama C2 (Nível de Containers)
```mermaid
graph TD
    User([Usuário / Cliente]) -->|HTTPS / Port 443| LB[Magalu Cloud Load Balancer]
    LB -->|HTTP / Port 80| Ingress[Ingress Controller - Nginx]
    Ingress -->|HTTP / Port 8080| App[API Container - Pod K8s]
    App -->|TCP / Port 5432 / TLS| DB[(PostgreSQL Gerenciado DBaaS)]
    Prometheus[Prometheus Server] -->|HTTP Scrape / Port 9090| App
    Prometheus -->|HTTP / Port 9090| Grafana[Grafana Dashboard]
