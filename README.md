
# Índice:

- Sobre o projeto
- Estrutura do projeto (resumo)
- Arquitetura e como o projeto funciona (visão prática)
  - Views (EJS)
  - Routes
  - Controllers
  - Models / Acesso ao banco
  - Seeders
  - Middleware
  - Sessões e autenticação
- Tecnologias
- Pré-requisitos
- Como clonar e configurar
  - Opção 1: Ambiente local
  - Opção 2: Dev Container (VS Code)
  - Opção 3: GitHub Codespaces
- Inicialização (seed)
- Rodando a aplicação
- Rotas principais
- Banco de dados (resumo)
- Troubleshooting
- Comandos úteis
- Contribuindo


# Sobre o projeto:

Este é um portal informativo sobre a neuro divergência, com uma gameficação relacionada ao tema e um banco de dados atrelado a gameficação. O objetivo é ser material didático para aprender sobre o tema, autenticação com sessões e acesso a banco MySQL via `workbench'.


## Estrutura do projeto (resumo)

Principais arquivos e pastas:

- node_modules/ — pasta automática com todas as dependências instaladas pelo NPM
- public/ — arquivos estáticos usados pelo front-end
- index.html — página principal do site NeuroDiverso
- script.js — lógica do front-end (quiz, interações etc.)
- styles.css — estilos e layout da aplicação
- db.js — configuração de acesso ao banco de dados (conexão MySQL)
- package-lock.json — versão travada das dependências instaladas
- package.json — scripts NPM e dependências do projeto
- server.js — arquivo principal do Node/Express, configura o servidor e as rotas.

# Arquitetura do projeto e como funciona(visão prática)

- Views:





