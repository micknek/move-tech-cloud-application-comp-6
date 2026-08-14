# ADR 0003: Adoção de Monolito Modular em vez de Microsserviços

- **Status:** Aprovado
- **Data:** 2026-08-14

## Contexto
No dimensionamento inicial da solução, avaliou-se dividir as funções do sistema em vários microsserviços independentes ou consolidar as regras de negócio em um Monolito Modular empacotado em um único contêiner de API.

## Decisão
Adotar a estratégia de Monolito Modular com empacotamento em contêiner único.

## Consequências
- **Positivas:**
  - Menor overhead de rede e menor latência interna (chamadas em memória em vez de requisições HTTP/gRPC entre serviços).
  - Pipeline de CI/CD simplificado com apenas uma imagem de contêiner.
  - Menor consumo de CPU/Memória, respeitando a meta de FinOps (R$ 150,00/mês).
- **Negativas:**
  - Todo o sistema precisa ser reimplantado a cada nova alteração.
  - Escalabilidade ocorre em nível de bloco completo, e não por função isolada.
