# Sistema de Venda de Ingressos – Paróquia Nossa Senhora da Esperança

> Aplicação web para venda, reserva e gestão de ingressos de espetáculos teatrais da paróquia.

---

## 📌 Visão geral

Este repositório contém o código-fonte do sistema interno de **venda e controle de ingressos**, com foco em:

- Compra on-line de ingressos;
- Controle de assentos e lotação do auditório;
- Emissão e envio de ingressos;
- Relatórios de acompanhamento de vendas para a equipe organizadora.

O sistema é totalmente independente e expõe uma **API REST**, que poderá ser consumida por qualquer frontend:  
site institucional, página HTML própria ou integração futura com WordPress.

---

## 🧱 Arquitetura do Sistema

O backend segue uma **Arquitetura em Camadas Orientada ao Domínio (DDD simplificado)**.

A aplicação é organizada em quatro camadas principais:

### ● 1. Presentation (API)
Responsável por:
- Controladores (controllers);
- Rotas da **API REST**;
- Validação e formatação de entrada e saída (DTOs).

Não contém lógica de negócio.

### ● 2. Application (Casos de Uso)
Contém os **use cases**, que coordenam o fluxo da aplicação:

- Criar pedido de ingresso;
- Validar disponibilidade de assentos;
- Registrar pagamento via PIX;
- Emitir e enviar ingressos;
- Gerar relatórios.

Aqui ficam apenas regras de aplicação, nunca regras de negócio.

### ● 3. Domain (Regras de Negócio)
A camada mais importante do sistema.

Inclui:
- **Entidades** (ex.: Espetáculo, Sessão, Assento, Pedido);
- **Value Objects** (ex.: CPF, Email);
- **Serviços de domínio**;
- **Interfaces de Repositórios**.

É totalmente independente de banco de dados, frameworks ou tecnologia externa.

### ● 4. Infrastructure (Implementações Técnicas)
Implementa tudo que é detalhe técnico:

- Repositórios concretos (ex.: SQL);
- Conexão com banco de dados (PostgreSQL recomendado);
- Integração com PIX;
- Envio de e-mails;
- Migrações;
- Configurações de ambiente.

---

## 🗂️ Estrutura de pastas (prevista)

```
/src
  /presentation
    /controllers
    /routes
    /dto
  /application
    /use_cases
  /domain
    /entities
    /value_objects
    /services
    /repositories   # apenas interfaces
  /infrastructure
    /database
    /repositories_impl
    /email
    /payment_pix
/tests
```

---

## 🎯 Objetivos do projeto

- Criar um fluxo simples, seguro e estável de venda de ingressos;
- Controlar assentos numerados do auditório;
- Oferecer uma interface sólida para o frontend consumir;
- Permitir relatórios de vendas para organizadores;
- Centralizar as regras de negócio dentro do domínio.

---

## 🧱 Tecnologias

- **Back-end:** Python (framework será definido entre FastAPI ou Django REST)
- **Banco de Dados:** PostgreSQL
- **API:** REST
- **Versão:** Git + GitHub

O backend é independente de qual frontend será usado.

---

## 👥 Equipe de Desenvolvimento

- Time com 3 desenvolvedores.
- Fluxo de trabalho:
  - Branch principal: `main`
  - Funcionalidades: `feature/nomedaregra`
  - Revisões via Pull Request

Mais detalhes em: `CONTRIBUTING.md`.

---

## 🚧 Como rodar o projeto (a ser atualizado)

Esta seção será atualizada assim que o framework for definido.  
A previsão é:

1. Clonar o repositório;
2. Criar/ativar ambiente virtual;
3. Instalar dependências;
4. Rodar servidor de desenvolvimento;
5. Rodar testes automáticos.

---

## 📌 Status

📍 Projeto em fase de **definição de arquitetura e estrutura inicial**.  
As próximas etapas serão:

- Escolha final do framework Python;
- Criação da estrutura base das camadas;
- Configuração do banco de dados;
- Implementação dos primeiros casos de uso.
