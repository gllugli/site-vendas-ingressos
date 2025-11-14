# Guia de Contribuição

Obrigado por colaborar com o Sistema de Venda de Ingressos da paróquia!  
Este documento descreve o fluxo de trabalho adotado no repositório, o padrão de branches e as boas práticas para desenvolvimento.

---

## 1. Fluxo de Trabalho (Git)

Usamos duas branches principais:

- **main** → versão estável (somente releases).
- **develop** → desenvolvimento contínuo.

### ✔ Regras centrais

1. **Ninguém faz commits diretamente em `main` ou `develop`.**
2. Todas as alterações devem ser criadas em uma branch própria.
3. **Todo Pull Request deve ser aberto para a branch `develop`.**
4. A branch `main` só recebe merges quando for gerar uma release estável.

---

## 2. Criando uma branch

Sempre criar sua branch A PARTIR DE `develop`:

```bash
git checkout develop
git pull origin develop
git checkout -b feature/nome-da-feature
```

### Exemplos de nomes válidos:

- `feature/checkout-ingressos`
- `feature/api-compra`
- `fix/corrige-envio-email`
- `fix/erro-validacao-cpf`

---

## 3. Abrindo um Pull Request (PR)

Antes de abrir o PR:

1. Atualize sua branch com a versão mais recente da develop:

```bash
git pull origin develop
```

2. Teste suas alterações.
3. Confirme que não há arquivos desnecessários no commit.
4. Abra um PR direcionado para:

```
base: develop
compare: sua-branch
```

5. Aguarde revisão de outro membro da equipe.

**Nunca abra PR diretamente para `main`.**

---

## 4. Padrão de Commits

Utilizamos mensagens de commit claras no formato:

```
tipo: descrição breve
```

Tipos permitidos:

- `feat:` → nova funcionalidade  
- `fix:` → correção de bug  
- `docs:` → alterações somente na documentação  
- `style:` → formatação e ajustes estéticos (sem mudar lógica)  
- `refactor:` → refatoração interna  
- `test:` → criação/ajuste de testes  
- `chore:` → tarefas auxiliares do projeto  

### Exemplos:

- `feat: cria endpoint de geração de ingresso`
- `fix: ajusta cálculo de assentos disponíveis`
- `docs: atualiza README com instruções de instalação`

---

## 5. Padrão de Código Python (PEP 8)

### ✔ Regras principais

- Indentação de **4 espaços**  
- Funções e variáveis em `snake_case`  
- Classes em `CamelCase`  
- Importações organizadas:
  1. Bibliotecas padrão
  2. Bibliotecas externas
  3. Módulos internos do projeto

### ✔ Docstrings

Todas as funções importantes devem possuir docstring:

```python
def calcular_valor(total, quantidade):
    """
    Calcula o valor total da compra.

    :param total: valor unitário do ingresso
    :param quantidade: quantidade de ingressos
    :return: valor final da compra
    """
```

### ✔ Type hints

Sempre que possível, utilize:

```python
def calcular_valor(total: float, quantidade: int) -> float:
    ...
```

---

## 6. Variáveis de Ambiente

- Nunca commitar credenciais, senhas ou chaves.
- Utilize `.env` localmente (não versionado).
- Utilize o arquivo `.env.example` como referência das variáveis necessárias.

---

## 7. Organização do Projeto

Estrutura inicial recomendada:

```
project/
 ├─ src/
 │   └─ app/
 │       ├─ routes/
 │       ├─ models/
 │       ├─ services/
 │       └─ utils/
 ├─ tests/
 ├─ docs/
 ├─ wordpress/
 ├─ requirements.txt
 ├─ .env.example
 └─ ...
```

---

## 8. Resumo Rápido

- Crie branches somente a partir de `develop`.
- Envie PRs sempre para `develop`.
- Siga o padrão de commits.
- Siga a PEP 8.
- Não commite segredos.
- PR para `main` apenas em releases.

Obrigado por contribuir! 🙌
