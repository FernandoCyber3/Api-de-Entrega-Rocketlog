# 🚀 Rocketlog - API de Gerenciamento de Entregas
 
O **Rocketlog** é uma solução robusta para o gerenciamento de encomendas, permitindo o controle total desde a criação do pedido até a entrega final. A API foi desenvolvida com foco em segurança, escalabilidade e rastreabilidade, utilizando padrões modernos como **RBAC** (Controle de Acesso Baseado em Funções) e **Logs de Eventos**.

---

## 🛠️ Tecnologias Utilizadas

O projeto utiliza o que há de mais moderno no ecossistema Node.js:

*   ![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white) **Runtime**
*   ![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white) **Linguagem**
*   ![Express](https://img.shields.io/badge/express.js-%23404d59.svg?style=for-the-badge&logo=express&logoColor=%2361DAFB) **Framework**
*   ![Prisma](https://img.shields.io/badge/Prisma-3982CE?style=for-the-badge&logo=Prisma&logoColor=white) **ORM**
*   ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white) **Banco de Dados**
*   ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) **Infraestrutura**
*   ![JWT](https://img.shields.io/badge/JWT-black?style=for-the-badge&logo=JSON%20web%20tokens) **Segurança**
*   ![Jest](https://img.shields.io/badge/-jest-%23C21325?style=for-the-badge&logo=jest&logoColor=white) **Testes**
*   ![Zod](https://img.shields.io/badge/Zod-3068b7?style=for-the-badge&logo=zod&logoColor=white) **Validação**

---

## ✨ Funcionalidades Principais

*   👤 **Gestão de Usuários:** Cadastro e autenticação com diferentes perfis (`customer` e `sale`).
*   📦 **Controle de Encomendas:** Criação, listagem e atualização de entregas.
*   🚦 **Ciclo de Status:** Fluxo completo de estados (`processing`, `shipped`, `delivered`, `canceled`).
*   📜 **Audit Log:** Registro detalhado de cada movimentação da encomenda para rastreabilidade.
*   🔐 **Segurança Avançada:** Proteção de rotas via JWT e autorização por perfil de usuário.
*   ✅ **Dados Blindados:** Validação rigorosa de entrada de dados com Zod.

---

## 🚀 Como Executar o Projeto

### Pré-requisitos
- Node.js instalado (v18 ou superior)
- Docker e Docker Compose

### Passo a Passo

**1. Clone o repositório:**
```bash
git clone https://github.com/FernandoCyber3/Api-de-Entrega-Rocketlog
cd Rocketlog
```

**2. Instale as dependências:**
```bash
npm install
```

**3. Configure o ambiente:**

Crie um arquivo `.env` na raiz do projeto com base no `.env-example` e configure suas variáveis:
```env
DATABASE_URL="postgresql://postgres:postgres@localhost:5432/rocketlog?schema=public"
JWT_SECRET="sua_chave_secreta_aqui"
```

**4. Suba o Banco de Dados (Docker):**
```bash
docker-compose up -d
```

**5. Execute as Migrations:**
```bash
npx prisma migrate deploy
```

**6. Inicie o Servidor:**
```bash
npm run dev
```

> O servidor estará disponível em: http://localhost:3333

---

## 🧪 Suíte de Testes

Para garantir a confiabilidade da aplicação, execute os testes automatizados:
```bash
npm run test:dev
```

---

## 📝 Guia de Rotas (Endpoints)

### 🔑 Autenticação & Usuários

| Método | Rota | Descrição | Acesso |
|---|---|---|---|
| `POST` | `/users` | Cadastro de novo usuário | Público |
| `POST` | `/sessions` | Login e geração de Token JWT | Público |

### 📦 Entregas (Deliveries)

| Método | Rota | Descrição | Perfil Requerido |
|---|---|---|---|
| `POST` | `/deliveries` | Criar nova encomenda | `sale` |
| `GET` | `/deliveries` | Listar todas as encomendas | `sale` |
| `PATCH` | `/deliveries/:id/status` | Atualizar status da entrega | `sale` |

### 📜 Logs de Eventos

| Método | Rota | Descrição | Perfil Requerido |
|---|---|---|---|
| `POST` | `/delivery-logs` | Registrar novo log na entrega | `sale` |
| `GET` | `/delivery-logs/:id/show` | Ver histórico de uma entrega | `sale` / `customer` |

---

## 🔒 Segurança (Auth)

Todas as rotas privadas exigem o envio do token no cabeçalho da requisição:
```http
Authorization: Bearer <seu_token_jwt>
```

## 📂 Estrutura do Projeto

```text
src/
 ├── controllers/    # Lógica de recebimento de requisições
 ├── middlewares/    # Filtros de segurança e validação
 ├── routes/         # Definição dos endpoints da API
 ├── database/       # Configuração de conexão (Prisma)
 ├── utils/          # Funções utilitárias e erros customizados
 ├── types/          # Definições de tipos TypeScript
 └── tests/          # Testes unitários e de integração
