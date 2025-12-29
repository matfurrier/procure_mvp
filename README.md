# Procure MVP – Solicitação & Cotação

🔗 **Languages:**  
- [Português 🇧🇷](#português)  
- [English 🇺🇸](#english)

📐 Diagramas: [Arquitetura e Fluxos](docs/diagrams/diagrams_Procure_MVP.md)
---

## Português

### Visão Geral

O **Procure MVP – Solicitação & Cotação** é um MVP interno desenvolvido para **substituir o fluxo de compras do BlueEz**, cobrindo todo o ciclo de **Solicitação → RFQ → Cotações → Aprovação → Sincronização com SAP B1**.

A solução foi desenhada para padronizar processos, aumentar rastreabilidade, reduzir retrabalho operacional e permitir evolução gradual para um fluxo corporativo mais robusto.

📌 **Status:** validação final / rollout  
📌 **Tipo:** sistema corporativo interno (MVP)  
📌 **Código-fonte:** privado (repositório público apenas para documentação)

---

### Problema

Antes do MVP:

- Solicitações de compra descentralizadas e pouco padronizadas  
- Fluxo de cotação dependente de e-mails e planilhas  
- Baixa rastreabilidade entre solicitação, RFQ e pedido  
- Dificuldade em comparar propostas de fornecedores  
- Integração manual ou inexistente com o SAP B1  
- Dependência de sistemas legados (BlueEz)  

---

### Solução

O Procure MVP permite:

- Criação estruturada de solicitações de compra  
- Geração automática de RFQs a partir de solicitações aprovadas  
- Convite de fornecedores com links públicos (sem login)  
- Registro de cotações internas ou externas  
- Mapa comparativo de preços por item e fornecedor  
- Seleção de vencedores (award)  
- Sincronização direta com SAP B1 Service Layer  
- Auditoria completa de status e transições  

---

### Fluxo Funcional (alto nível)

1. Usuário cria uma **Solicitação de Compra**  
2. Solicitação passa por **aprovação**  
3. Comprador gera uma **RFQ**  
4. Fornecedores são convidados via **link público**  
5. Cotações são recebidas e comparadas  
6. Comprador define **award** (vencedores)  
7. Pedido é sincronizado com o **SAP B1**  

---

### Arquitetura (alto nível)

```
[ Next.js Web ]
        |
        v
[ FastAPI API ]
        |
 -----------------------------
 |             |             |
[ PostgreSQL ] [ PostgreSQL ] [ SAP B1 ]
[ procure_mvp ][ security ]  [ Service Layer ]
```

- Frontend desacoplado
- Backend stateless com JWT
- Banco transacional separado do banco de segurança
- Integração ERP via Service Layer

---

### Stack Tecnológico

**Backend**
- Python 3.11
- FastAPI
- SQLAlchemy
- PostgreSQL
- JWT (local) + roadmap Keycloak
- Integração SAP B1 Service Layer

**Frontend**
- Next.js
- React
- TypeScript
- Tailwind CSS

**Infraestrutura**
- Docker
- Docker Compose

---

### Segurança e Governança

- Autenticação JWT
- Fallback local com Argon2
- Tokens públicos controlados para fornecedores
- Validações server-side de status e permissões
- Log de transições (status_log)
- Separação de schema de segurança

---

### Papel de Liderança Técnica

Neste MVP, atuei como responsável por:

- Arquitetura da solução end-to-end  
- Definição do fluxo funcional M1 → M3  
- Modelagem de dados e status  
- Governança de segurança e acessos  
- Estratégia de integração com SAP B1  
- Estruturação do MVP para evolução futura  
- Entrega técnica completa  

---

### Prints e Diagramas

📁 `/docs/images`  
- Prints com dados borrados ou mockados  
- Diagramas de arquitetura e fluxos (Mermaid)

---

### Observações

- Código mantido privado por se tratar de sistema corporativo  
- Este repositório existe para documentação e apresentação técnica  

---

## English

### Overview

**Procure MVP – Solicitation & Quotation** is an internal MVP designed to **replace the BlueEz purchasing workflow**, covering the full cycle from **Purchase Request → RFQ → Quotes → Approval → SAP B1 synchronization**.

📌 **Status:** final validation / rollout  
📌 **Type:** internal corporate MVP  
📌 **Source code:** private (public repository for documentation only)

---

### Problem

Before this MVP:

- Decentralized purchase requests  
- Quotation process based on emails and spreadsheets  
- Low traceability across purchasing stages  
- Difficult supplier price comparison  
- Manual or missing SAP B1 integration  
- Dependency on legacy systems  

---

### Solution

The Procure MVP enables:

- Structured purchase requests  
- Automatic RFQ generation  
- Supplier invitations via public links  
- Internal and external quote submissions  
- Comparative pricing map  
- Award definition  
- Direct SAP B1 Service Layer synchronization  
- Full audit trail of status transitions  

---

### High-Level Flow

1. User creates a purchase request  
2. Request is approved  
3. Buyer generates an RFQ  
4. Suppliers receive public invitation links  
5. Quotes are submitted and compared  
6. Award is defined  
7. Order is synced with SAP B1  

---

### Architecture (high level)

```
[ Next.js Web ]
        |
        v
[ FastAPI API ]
        |
 -----------------------------
 |             |             |
[ PostgreSQL ] [ PostgreSQL ] [ SAP B1 ]
[ procure_mvp ][ security ]  [ Service Layer ]
```

---

### Technology Stack

**Backend**
- Python 3.11
- FastAPI
- SQLAlchemy
- PostgreSQL
- JWT + Keycloak roadmap
- SAP B1 Service Layer

**Frontend**
- Next.js
- React
- TypeScript
- Tailwind CSS

**Infrastructure**
- Docker
- Docker Compose

---

### Security & Governance

- JWT authentication
- Argon2 local fallback
- Controlled public tokens
- Server-side validations
- Status audit log
- Dedicated security schema

---

### Technical Leadership

Responsibilities in this project included:

- End-to-end architecture
- Functional flow design
- Data modeling
- Security and access governance
- SAP B1 integration strategy
- MVP structuring for scalability
- Full technical delivery

---

### Screenshots & Diagrams

📁 `/docs/images`  
All images use blurred or mocked data for demonstration.

---

### Notes

- Source code is private due to corporate ownership  
- This repository exists for technical documentation and professional presentation  
