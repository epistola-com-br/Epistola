# 📁 Estrutura do Projeto - Epístola

Este documento descreve a organização de pastas e arquivos do projeto Epístola.

```
epistola/
├── 📄 README.md                    # Documentação principal
├── 📄 LICENSE                      # Licença MIT
├── 📄 MILESTONES.md                # Marcos de desenvolvimento
├── 📄 ISSUES.md                    # Lista de issues/features
├── 📄 ROADMAP.md                   # Timeline do projeto
├── 📄 CONTRIBUTING.md              # Guia de contribuição
├── 📄 CHANGELOG.md                 # Histórico de mudanças
├── 📄 .gitignore                   # Arquivos ignorados pelo Git
├── 📄 package.json                 # Dependências e scripts
├── 📄 docker-compose.yml           # Configuração de containers
├── 📄 Dockerfile                   # Imagem Docker
│
├── 📁 .github/                     # Configurações do GitHub
│   ├── 📁 ISSUE_TEMPLATE/          # Templates de issues
│   │   ├── bug_report.md
│   │   ├── feature_request.md
│   │   └── documentation.md
│   ├── 📁 workflows/               # GitHub Actions
│   │   ├── ci.yml
│   │   ├── deploy.yml
│   │   └── security.yml
│   └── 📄 pull_request_template.md # Template de PR
│
├── 📁 docs/                        # Documentação
│   ├── 📄 architecture.md          # Arquitetura do sistema
│   ├── 📄 api.md                   # Documentação da API
│   ├── 📄 integration.md           # Guia de integração
│   ├── 📄 deployment.md            # Guia de deploy
│   ├── 📄 security.md              # Documentação de segurança
│   └── 📁 assets/                  # Imagens e diagramas
│       ├── architecture-diagram.png
│       └── api-flow.png
│
├── 📁 src/                         # Código fonte
│   ├── 📁 api/                     # Backend/APIs
│   │   ├── 📁 auth/                # Serviço de autenticação
│   │   │   ├── controllers/
│   │   │   ├── services/
│   │   │   ├── models/
│   │   │   └── routes/
│   │   ├── 📁 users/               # Serviço de usuários
│   │   ├── 📁 wallets/             # Serviço de carteiras
│   │   ├── 📁 missivas/            # Serviço de cartas
│   │   ├── 📁 epistolarios/        # Serviço de Epistolários
│   │   ├── 📁 shared/              # Código compartilhado
│   │   │   ├── middleware/
│   │   │   ├── utils/
│   │   │   ├── config/
│   │   │   └── database/
│   │   └── 📄 server.js            # Servidor principal
│   │
│   ├── 📁 web/                     # Frontend web
│   │   ├── 📁 components/          # Componentes React
│   │   ├── 📁 pages/               # Páginas Next.js
│   │   ├── 📁 hooks/               # Custom hooks
│   │   ├── 📁 store/               # Estado global
│   │   ├── 📁 styles/              # CSS/Tailwind
│   │   ├── 📁 utils/               # Utilitários
│   │   └── 📄 next.config.js       # Configuração Next.js
│   │
│   └── 📁 shared/                  # Código compartilhado
│       ├── 📁 types/               # TypeScript types
│       ├── 📁 constants/           # Constantes
│       ├── 📁 validators/          # Validações
│       └── 📁 sdk/                 # SDK para integração
│
├── 📁 tests/                       # Testes
│   ├── 📁 unit/                    # Testes unitários
│   ├── 📁 integration/             # Testes de integração
│   ├── 📁 e2e/                     # Testes end-to-end
│   ├── 📁 fixtures/                # Dados de teste
│   └── 📄 setup.js                 # Configuração de testes
│
├── 📁 scripts/                     # Scripts utilitários
│   ├── 📄 setup.sh                 # Setup inicial
│   ├── 📄 migrate.js               # Migrações de DB
│   ├── 📄 seed.js                  # Dados iniciais
│   └── 📄 deploy.sh                # Script de deploy
│
├── 📁 config/                      # Configurações
│   ├── 📄 database.js              # Config do banco
│   ├── 📄 redis.js                 # Config do Redis
│   ├── 📄 auth.js                  # Config de autenticação
│   └── 📄 app.js                   # Config da aplicação
│
├── 📁 migrations/                  # Migrações de banco
│   ├── 001_create_users.sql
│   ├── 002_create_epistolarios.sql
│   └── 003_create_missivas.sql
│
├── 📁 public/                      # Arquivos públicos
│   ├── 📁 images/                  # Imagens
│   ├── 📁 icons/                   # Ícones
│   └── 📄 favicon.ico              # Favicon
│
└── 📁 deployments/                 # Configurações de deploy
    ├── 📁 kubernetes/              # Manifests K8s
    ├── 📁 terraform/               # Infraestrutura
    └── 📁 docker/                  # Configs Docker
```

## 📝 Convenções de Nomenclatura

### Arquivos
- **kebab-case**: `user-service.js`, `api-routes.js`
- **camelCase**: Para variáveis e funções
- **PascalCase**: Para classes e componentes React
- **UPPER_CASE**: Para constantes e variáveis de ambiente

### Pastas
- **kebab-case**: `user-management/`, `email-templates/`
- **Plural**: Para coleções (`users/`, `missivas/`)
- **Singular**: Para módulos (`auth/`, `config/`)

### Branches
- **feature/**: `feature/auth-oauth-flow`
- **fix/**: `fix/wallet-balance-calculation`
- **docs/**: `docs/api-documentation-update`
- **refactor/**: `refactor/database-optimization`

### Commits
- **feat**: Nova funcionalidade
- **fix**: Correção de bug
- **docs**: Documentação
- **style**: Formatação/estilo
- **refactor**: Refatoração
- **test**: Testes
- **chore**: Tarefas auxiliares

## 🎯 Organização por Funcionalidade

### Auth Service (`src/api/auth/`)
```
auth/
├── controllers/
│   ├── auth.controller.js          # Login, register, logout
│   └── oauth.controller.js         # OAuth para Epistolários
├── services/
│   ├── auth.service.js             # Lógica de autenticação
│   ├── jwt.service.js              # Gerenciamento JWT
│   └── oauth.service.js            # Lógica OAuth
├── models/
│   ├── user.model.js               # Modelo de usuário
│   └── application.model.js        # Modelo de aplicação OAuth
├── routes/
│   ├── auth.routes.js              # Rotas de autenticação
│   └── oauth.routes.js             # Rotas OAuth
└── middleware/
    ├── auth.middleware.js          # Verificação de token
    └── rate-limit.middleware.js    # Rate limiting
```

### Frontend Structure (`src/web/`)
```
web/
├── components/
│   ├── ui/                         # Componentes básicos
│   │   ├── Button.tsx
│   │   ├── Input.tsx
│   │   └── Modal.tsx
│   ├── auth/                       # Componentes de auth
│   │   ├── LoginForm.tsx
│   │   └── RegisterForm.tsx
│   ├── missivas/                   # Componentes de cartas
│   │   ├── MissivaCard.tsx
│   │   └── MissivaGrid.tsx
│   └── layout/                     # Layout components
│       ├── Header.tsx
│       ├── Footer.tsx
│       └── Sidebar.tsx
├── pages/
│   ├── index.tsx                   # Homepage
│   ├── auth/
│   │   ├── login.tsx
│   │   └── register.tsx
│   ├── dashboard/
│   │   └── index.tsx
│   └── epistolarios/
│       ├── index.tsx
│       └── [id].tsx
└── hooks/
    ├── useAuth.ts                  # Hook de autenticação
    ├── useWallet.ts                # Hook de carteira
    └── useMissivas.ts              # Hook de cartas
```

## 🔧 Configuração de Desenvolvimento

### Environment Variables
```env
# Database
DATABASE_URL=postgresql://user:pass@localhost:5432/epistola
REDIS_URL=redis://localhost:6379

# JWT
JWT_SECRET=your-super-secret-key
JWT_EXPIRES_IN=1h

# OAuth
OAUTH_ENCRYPTION_KEY=32-char-key

# External Services
STRIPE_SECRET_KEY=sk_test_...
SMTP_HOST=smtp.mailgun.org
SMTP_USER=postmaster@mg.epistola.com.br
SMTP_PASS=your-smtp-password

# Storage
AWS_S3_BUCKET=epistola-assets
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key

# Application
NODE_ENV=development
PORT=3000
API_BASE_URL=http://localhost:3000
WEB_BASE_URL=http://localhost:3001
```

## 📦 Package Management

### Backend Dependencies
```json
{
  "dependencies": {
    "express": "^4.18.0",
    "fastify": "^4.0.0",
    "typeorm": "^0.3.0",
    "redis": "^4.5.0",
    "jsonwebtoken": "^9.0.0",
    "bcrypt": "^5.1.0",
    "joi": "^17.7.0",
    "stripe": "^11.0.0"
  },
  "devDependencies": {
    "jest": "^29.0.0",
    "supertest": "^6.3.0",
    "eslint": "^8.0.0",
    "prettier": "^2.8.0"
  }
}
```

### Frontend Dependencies
```json
{
  "dependencies": {
    "react": "^18.0.0",
    "next": "^13.0.0",
    "tailwindcss": "^3.2.0",
    "zustand": "^4.0.0",
    "react-hook-form": "^7.0.0",
    "zod": "^3.20.0"
  },
  "devDependencies": {
    "@types/react": "^18.0.0",
    "typescript": "^4.9.0",
    "eslint-config-next": "^13.0.0"
  }
}
```

## 🚀 Scripts Principais

```json
{
  "scripts": {
    "dev": "concurrently \"npm run dev:api\" \"npm run dev:web\"",
    "dev:api": "nodemon src/api/server.js",
    "dev:web": "cd src/web && npm run dev",
    "build": "npm run build:api && npm run build:web",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage",
    "lint": "eslint src/",
    "lint:fix": "eslint src/ --fix",
    "migrate": "node scripts/migrate.js",
    "seed": "node scripts/seed.js",
    "docker:up": "docker-compose up -d",
    "docker:down": "docker-compose down"
  }
}
```

---

*Esta estrutura será implementada gradualmente conforme o desenvolvimento do projeto.*