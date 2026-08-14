# ADR 0001: Banco de Dados Fora do Cluster Kubernetes (DBaaS)

- **Status:** Aprovado
- **Data:** 2026-08-14

## Contexto
A aplicação necessita de persistência de dados relacional (PostgreSQL) com alta integridade, suporte a snapshots/backups contínuos e recuperação de falhas sem intervenção manual complexa. Havia a opção de executar o banco dentro do cluster K8s (StatefulSet com volumes PVC) ou utilizar uma instância gerenciada na Magalu Cloud.

## Decisão
Adotar o PostgreSQL Gerenciado (DBaaS) fora do cluster Kubernetes.

## Consequências
- **Positivas:**
  - Redução drástica da complexidade operacional do cluster (sem necessidade de gerenciar storage classes de alta performance e volumes persistentes).
  - Rotinas automatizadas de backup e recuperação gerenciadas pelo provedor de nuvem.
  - O cluster Kubernetes permanece stateless (sem estado), simplificando reinicializações e atualizações.
- **Negativas:**
  - Custo financeiro ligeiramente superior ao de hospedar o banco no próprio nó.
  - Necessidade de configuração de regras de rede (Security Groups / VPC) para permitir acesso seguro entre o cluster e o DBaaS.
