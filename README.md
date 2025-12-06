## Índice

- Sobre o projeto
- Estrutura do projeto (resumo)
- Arquitetura e como o projeto funciona (visão prática)
  - Routes
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

_____


## Sobre o projeto

Este é um portal informativo sobre neuro divergência. Nosso objetivo é criar um material didático sobre o conteúdo, utilizando para isso node.js, javascript, MySQL, Css e HTML.

__________

## Estrutura do projeto (resumo)

Principais arquivos e pastas:

node_modules/ — pasta automática com todas as dependências instaladas pelo NPM

public/ — arquivos estáticos usados pelo front-end

index.html — página principal do site NeuroDiverso

script.js — lógica do front-end (quiz, interações etc.)

styles.css — estilos e layout da aplicação

package-lock.json — versão travada das dependências instaladas

package.json — scripts NPM e dependências do projeto

db.js — configuração de acesso ao banco de dados (conexão MySQL)

server.js — arquivo principal do Node/Express, configura o servidor e as rotas

___________

## Arquitetura e como o projeto funciona (visão prática)

### Routes (rotas)

Todas as rotas estão definidas diretamente dentro do arquivo server.js. 
São elas: Rota principal, cadastro, teste de conexão, login e Quiz.

Trecho (resumido):

```js
// rota principal
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
});
// cadastro
app.post('/api/auth/register', async (req, res) => {
  try {
    const { name, email, password } = req.body;
// teste de conexão
app.get('/api/test-db', async (req, res) => {
  try {
    const [rows] = await db.query('SELECT 1 AS ok');
    res.json({ ok: true, db: rows });
// login
app.post('/api/auth/login', async (req, res) => {
  try {
    const { email, password } = req.body;
/* ==================== QUIZ ==================== */

app.post('/api/quiz/score', async (req, res) => {
  try {
    const { userId, pontuacao } = req.body;

```

### Middleware

Estão todos no server js. Exemplos no projeto:

app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(express.static('public'));

## Tecnologias

- Node.js
- Express.js
- HTML 
- MySQL (via `mysql2`)
- bcrypt (hash de senhas)
- Css

## Pré-requisitos

- Node.js (recomenda-se v18+ ou v24)
- npm
- MySQL 8.0+ (ou um serviço compatível)
- VS Code (opcional, recomendado para usar Dev Container)

## Como clonar e configurar

Opção 1 — Ambiente local

 1. O que a pessoa precisa ter antes

VS Code instalado

Baixa em: https://code.visualstudio.com

Node.js instalado

Baixa em: https://nodejs.org

Depois pode conferir a versão no terminal:

node -v
npm -v


MySQL instalado e rodando

MySQL Server + (opcional) MySQL Workbench.

O banco neurodivergencias e as tabelas já devem ter sido criadas com aquele script SQL que montamos.

O projeto já baixado/descompactado em alguma pasta (ex: Downloads/NEURO_FINAL).

2. Abrir o projeto no VS Code

Abra o VS Code.

Clique em File (Arquivo) → Open Folder (Abrir Pasta).

Selecione a pasta do projeto, por exemplo:

C:\Users\SeuUsuario\Downloads\NEURO_FINAL

Clique em Select Folder.

No Explorer do VS Code (lado esquerdo) a pessoa deve ver algo tipo:

NEURO_FINAL
  ├─ node_modules/    (aparece depois do npm install)
  ├─ public/
  │   ├─ html/
  │   │   └─ index.html
  │   ├─ script.js
  │   └─ styles.css
  ├─ db.js
  ├─ server.js
  ├─ package.json
  └─ package-lock.json

3. Conferir a conexão com o banco (db.js)

Ainda no VS Code:

Clique em db.js.

A pessoa vai ver algo assim:

const mysql = require('mysql2/promise');

const pool = mysql.createPool({
  host: 'localhost',
  user: 'root',
  password: 'SUA_SENHA_AQUI',
  database: 'neurodivergencias'
});

module.exports = pool;


Ela precisa ajustar user e password para os dados do MySQL dela:

user: 'root' (ou outro usuário)

password: 'senha_do_mysql'

Se o banco tiver outro nome, também ajusta database.

4. Abrir o terminal integrado no VS Code

No topo do VS Code, clique em:
Terminal → New Terminal (Novo Terminal).

Vai abrir um terminal embaixo. O caminho (prompt) deve terminar com algo tipo:

...\NEURO_FINAL>


Se não estiver dentro da pasta do projeto, a pessoa pode entrar com:

cd caminho/para/NEURO_FINAL


Exemplo no Windows:

cd C:\Users\User\Downloads\NEURO_FINAL

5. Instalar as dependências do projeto

No terminal do VS Code (dentro da pasta do projeto), rodar:

npm install


Isso vai ler o package.json e baixar tudo que o projeto precisa (express, mysql2, bcryptjs, etc.) dentro da pasta node_modules.

Esse comando é feito uma vez (ou quando adicionar novas libs).

6. Garantir que o MySQL está rodando

Antes de subir o servidor:

Abrir o MySQL Workbench (ou outro cliente).

Conectar no MySQL.

Rodar:

SHOW DATABASES;


Verificar se aparece neurodivergencias.
Se não existir, criar o banco e as tabelas com o script SQL que você já montou.

7. Rodar o servidor Node pelo VS Code

No terminal integrado (ainda dentro de NEURO_FINAL), rodar:

npm start


Se no package.json tiver "start": "node server.js", esse comando já resolve.
Se não tiver script, pode usar diretamente:

node server.js


Se tudo der certo, vai aparecer algo no terminal como:

Servidor rodando em http://localhost:3000

8. Abrir o site no navegador

Com o servidor rodando, a pessoa abre o navegador (Chrome, Edge etc.) e digita:

http://localhost:3000


Ali ela já vai ver o seu site NeuroDiverso carregado.

9. Testar rapidamente a conexão com o banco

Se quiser testar só o banco:

Com o servidor ligado, acessar:

http://localhost:3000/api/test-db


Se aparecer algo como:

{"ok":true,"db":[{"ok":1}]}


➜ Node está falando com o MySQL certinho.

10. Como parar o servidor pelo VS Code

No terminal integrado do VS Code, onde o servidor está rodando:

Pressionar Ctrl + C

Confirmar com Y se pedir (no Windows)

O prompt volta ao normal e a porta 3000 fica liberada.

11. Resumão dos comandos que a outra pessoa vai usar

Dentro da pasta do projeto (NEURO_FINAL), no terminal do VS Code:

# 1 vez (instalar dependências)
npm install

# sempre que quiser rodar o site
npm start
# ou
node server.js


Navegador:

Site: http://localhost:3000

Teste do banco: http://localhost:3000/api/test-db
---


## Rodando a aplicação

- Desenvolvimento: `npm run dev` (nodemon)
- Produção: `npm start`

## Rotas principais

Rotas públicas:

- `GET /` — listagem pública de notícias
- `GET /noticia/:id` — visualizar notícia
- `GET /login` — formulário de login
- `POST /login` — processa login

Rotas admin (requer login):

- `GET /admin` — dashboard
- `GET/POST /admin/noticias` — CRUD de notícias (via routes)
- `GET/POST /admin/usuarios` — gerenciar usuários (admin)

## Banco de dados (resumo das tabelas)

1. O que precisa estar instalado

A outra pessoa precisa ter:

Node.js (de preferência versão 18+)

Baixar em: https://nodejs.org

Ao instalar o Node, o npm vem junto.

MySQL Server + MySQL Workbench

MySQL Server = o banco em si

MySQL Workbench = programa gráfico para criar banco/tabelas e ver os dados.

(Opcional, mas recomendado) VS Code

Para abrir o projeto de forma organizada.

2. Como baixar e abrir o projeto

Baixar o projeto (por Git ou .zip):

git clone <URL_DO_REPOSITORIO>
cd neuro_final


ou descompactar o .zip e depois abrir a pasta no VS Code.

Dentro da pasta do projeto (onde está package.json), rodar:

npm install


Isso vai instalar as dependências que o projeto usa:

express

mysql2

bcryptjs

(e o que mais tiver no package.json)

3. Criar o banco de dados e as tabelas

No MySQL Workbench (ou no terminal do MySQL), a pessoa precisa rodar esse script:

-- 1. Criar o banco
CREATE DATABASE neurodivergencias;
USE neurodivergencias;

-- 2. Tabela de usuários
CREATE TABLE users (
  id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
  nome VARCHAR(255) NOT NULL,
  email VARCHAR(255) NOT NULL UNIQUE,
  senha_hash VARCHAR(255) NOT NULL,
  criado_em TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 3. Tabela de pontuações do quiz
CREATE TABLE quiz_scores (
  id INT PRIMARY KEY AUTO_INCREMENT,
  user_id INT NOT NULL,
  pontuacao INT NOT NULL,
  respondido_em DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id)
);

-- 4. Tabela de perguntas
CREATE TABLE quiz_questions (
  id INT PRIMARY KEY AUTO_INCREMENT,
  pergunta TEXT NOT NULL,
  opcao_a VARCHAR(255) NOT NULL,
  opcao_b VARCHAR(255) NOT NULL,
  opcao_c VARCHAR(255) NOT NULL,
  opcao_d VARCHAR(255) NOT NULL,
  correta ENUM('A', 'B', 'C', 'D') NOT NULL,
  categoria VARCHAR(100),
  ativa TINYINT(1) DEFAULT 1
);

-- 5. Tabela de badges
CREATE TABLE badges (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nome VARCHAR(100) NOT NULL,
  descricao VARCHAR(255),
  requisito_pontuacao INT NOT NULL
);

-- 6. Tabela que liga usuário x badge conquistada
CREATE TABLE user_badges (
  id INT PRIMARY KEY AUTO_INCREMENT,
  user_id INT NOT NULL,
  badge_id INT NOT NULL,
  conquistado_em DATETIME DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id),
  FOREIGN KEY (badge_id) REFERENCES badges(id)
);

-- 7. Tabela de respostas do quiz (detalhe de cada questão respondida)
CREATE TABLE quiz_answers (
  id INT PRIMARY KEY AUTO_INCREMENT,
  score_id INT NOT NULL,
  question_id INT NOT NULL,
  alternativa_marcada ENUM('A','B','C','D') NOT NULL,
  correta TINYINT(1) NOT NULL,
  FOREIGN KEY (score_id) REFERENCES quiz_scores(id),
  FOREIGN KEY (question_id) REFERENCES quiz_questions(id)
);


Depois disso, o banco está pronto para falar com o Node.

4. Como está configurada a integração do banco no código

No arquivo db.js (na raiz do projeto), você tem algo assim:

// db.js - módulo de conexão com o MySQL
const mysql = require('mysql2/promise');

const pool = mysql.createPool({
  host: 'localhost',   // HOST DO BANCO
  user: 'root',        // USUÁRIO DO MYSQL
  password: '12345',  // SENHA DO MYSQL
  database: 'neurodivergencias' // NOME DO BANCO
});

module.exports = pool;

 O que outra pessoa precisa ajustar aqui?

Se na máquina dela o usuário do MySQL for diferente de root, ela troca:

user: 'root',


Se a senha dela não for 12345, troca:

password: 'SENHA_DA_PESSOA',


Se o banco tiver outro nome, troca:

database: 'neurodivergencias',

Sobre o host

host: 'localhost' significa que o banco está rodando na mesma máquina do Node.

Poderia ser também:

127.0.0.1 → mesmo computador

IP de outro servidor → ex: 192.168.0.10

Nome de serviço em Docker → ex: db

Então, para “fazer o comando de host”, na prática, é editar essa linha conforme onde o MySQL está rodando.

5. Rodar o servidor Node

Depois que:

MySQL estiver rodando,

Banco e tabelas tiverem sido criados,

db.js estiver com as credenciais certas,

a pessoa vai até a pasta do projeto e roda:

npm start


(seu package.json provavelmente tem "start": "node server.js")

Ou então:

node server.js


Se estiver tudo certo, o terminal vai mostrar algo como:

Servidor rodando em http://localhost:3000

6. Como a outra pessoa testa se a integração com o banco funcionou
 Teste 1 – Rota de teste do banco

No navegador, acessar:

http://localhost:3000/api/test-db


Se a resposta for algo como:

{"ok":true,"db":[{"ok":1}]}


 Node conseguiu conversar com o MySQL.

Se der erro 500, provavelmente é:

credencial errada em db.js

banco não existe

MySQL desligado

 Teste 2 – Cadastro de usuário

Abrir o site:

http://localhost:3000


Usar o modal de Criar conta do próprio site.

Depois, no MySQL Workbench, rodar:

USE neurodivergencias;
SELECT * FROM users;


Se aparecer o usuário que foi cadastrado:

 front → backend → banco de dados funcionando.

 Teste 3 – Salvar pontuação

Fazer login.

Realizar o quiz até o final.

No MySQL:

SELECT * FROM quiz_scores;



## Comandos úteis

- `npm install` — instala dependências
- `npm run seed` — cria tabelas e insere dados de exemplo
- `npm run dev` — executa em modo dev com `nodemon`
- `npm start` — inicia com `node app.js`

## Contribuindo

Contribuições são bem-vindas. Passos sugeridos:

1. Fork
2. Crie uma branch `feature/descricao`
3. Commit e push
4. Abra PR

Pequenas melhorias possíveis: adicionar upload de imagens, paginação, API REST JSON, testes automatizados.
- `npm install` — instala dependências



