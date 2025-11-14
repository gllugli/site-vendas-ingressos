# Arquitetura do Projeto – Sistema de Venda de Ingressos

Este documento descreve a arquitetura inicial do projeto, a organização das pastas e as regras fundamentais para manter o código limpo, modular e escalável.  
A API em Python será consumida pelo WordPress, que funcionará como interface pública do sistema.

---

## 1. Objetivo da Arquitetura

A arquitetura foi planejada para:

- Separar claramente responsabilidades (rotas, regras de negócio, banco, integrações).
- Facilitar o crescimento do projeto sem gerar acoplamento.
- Organizar funcionalidades por domínio (ex.: ingressos, eventos, pagamentos).
- Permitir que o time colabore sem conflitos.
- Tornar mais simples testar, revisar e manter o código.

---

## 2. Visão Geral da Estrutura de Pastas

```
src/
 └─ app/
     ├─ main.py
     ├─ core/
     │   ├─ config.py
     │   └─ database.py
     ├─ ingressos/
     │   ├─ routes.py
     │   ├─ service.py
     │   ├─ repository.py
     │   └─ schemas.py
     ├─ eventos/
     │   ├─ routes.py
     │   ├─ service.py
     │   ├─ repository.py
     │   └─ schemas.py
     ├─ usuarios/
     │   ├─ routes.py
     │   ├─ service.py
     │   ├─ repository.py
     │   └─ schemas.py
     ├─ pagamentos/
     │   ├─ service.py
     │   └─ integrations.py
     ├─ integrations/
     │   └─ wordpress.py
     └─ utils/
         └─ email_sender.py
tests/
docs/
wordpress/
requirements.txt
.env.example
```

---

## 3. Descrição das Pastas

### **3.1. `src/app/main.py`**
Arquivo principal que inicializa a aplicação (cria servidor, registra rotas, configurações e banco).

---

### **3.2. `core/`**
Contém tudo que é fundamental para rodar o sistema:

- `config.py`:  
  Carrega variáveis do `.env`, configura banco, email, chaves, etc.

- `database.py`:  
  Conexão com o banco, sessões, inicialização de tabelas.

---

### **3.3. Pastas de Domínio**

Cada domínio tem a mesma estrutura interna:

```
dominio/
 ├─ routes.py      -> endpoints (HTTP)
 ├─ service.py     -> regras de negócio
 ├─ repository.py  -> banco de dados
 └─ schemas.py     -> modelos de entrada/saída
```

#### **routes.py**
- Recebe HTTP do WordPress
- Valida entrada
- Chama o service
- Retorna resposta HTTP

---

#### **service.py**
Onde mora a lógica do sistema:

- Reservar ingresso  
- Validar informações  
- Processar pedidos  
- Disponibilidade de assentos  

---

#### **repository.py**
- CRUD no banco de dados
- Consultas simples
- Nada de lógica de negócio

---

#### **schemas.py**
Define formatos dos dados usando Pydantic ou dataclasses.

---

### **3.4. `integrations/`**
Código que acessa APIs externas, como WordPress.

---

### **3.5. `utils/`**
Funções genéricas e auxiliares (email, datas, código, helpers).

---

## 4. Fluxo Ideal da Aplicação

```
WordPress → routes → service → repository → banco
```

Regras importantes:

- Rotas não fazem SQL  
- Services não retornam HTTP  
- Repositórios não aplicam regras  

---

## 5. Como Criar Novas Funcionalidades

1. Criar pasta ou arquivos no domínio correto  
2. Adicionar:
   - rota  
   - service  
   - repository  
   - schema  
3. Criar testes em `tests/`  
4. Abrir PR para `develop`  

---

## 6. Quando Dividir Módulos Grandes

Se um domínio crescer demais, quebrar em:

```
ingressos/
 ├─ reserva_service.py
 ├─ checkin_service.py
 ├─ repository.py
 └─ routes.py
```

---

## 7. Integração com WordPress

O WordPress acessa apenas **rotas HTTP**.

Fluxo:

1. WP envia requisição  
2. API processa  
3. Banco atualiza  
4. API devolve status  

Se API precisar chamar WP → usar `integrations/wordpress.py`.

---

## 8. Boas Práticas

- Separação clara de responsabilidades.  
- Documentar decisões em `docs/`.  
- Manter estrutura consistente.  
- Criar testes junto com cada feature.  
- Evitar transformar `utils/` em lixeira de funções.  

---

## 9. Resumo

Arquitetura pensada para:

- Crescer sem virar bagunça  
- Ser fácil de entender  
- Facilitar manutenção  
- Integrar corretamente com WordPress  
- Ajudar onboarding de novos devs  

Essa estrutura é a base do desenvolvimento inicial.
