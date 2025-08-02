# 🚀 Guia de Desenvolvimento - Focus Todo Turbinado

## 🎯 Visão Geral

Este guia fornece todas as informações necessárias para desenvolvedores contribuírem com o projeto Focus Todo Turbinado, desde a configuração do ambiente até as melhores práticas de desenvolvimento.

## 📋 Pré-requisitos

### Software Necessário
- **Node.js**: 18.17.0 ou superior
- **npm**: 9.0.0 ou superior
- **PostgreSQL**: 14.0 ou superior
- **Redis**: 7.0 ou superior
- **Git**: 2.30.0 ou superior

### Contas Necessárias
- **OpenAI**: Para API do ChatGPT
- **GitHub**: Para versionamento
- **Vercel**: Para deploy do frontend (opcional)
- **Railway**: Para deploy do backend (opcional)

## 🛠️ Configuração do Ambiente

### 1. Clone do Repositório
```bash
git clone https://github.com/seu-usuario/focus-todo-turbinado.git
cd focus-todo-turbinado
```

### 2. Instalação de Dependências
```bash
# Instalar dependências do projeto
npm install

# Instalar dependências do frontend
cd frontend && npm install

# Instalar dependências do backend
cd ../backend && npm install

# Voltar para a raiz
cd ..
```

### 3. Configuração do Banco de Dados
```bash
# Criar banco PostgreSQL
createdb focus_todo_dev

# Executar migrações
cd backend
npm run db:migrate

# Executar seeds (dados iniciais)
npm run db:seed
```

### 4. Configuração do Redis
```bash
# Iniciar Redis (se não estiver rodando como serviço)
redis-server

# Verificar se está funcionando
redis-cli ping
```

### 5. Variáveis de Ambiente
```bash
# Copiar arquivo de exemplo
cp .env.example .env

# Editar variáveis de ambiente
nano .env
```

**Exemplo de `.env`:**
```env
# Database
DATABASE_URL="postgresql://user:password@localhost:5432/focus_todo_dev"
REDIS_URL="redis://localhost:6379"

# OpenAI
OPENAI_API_KEY="your-openai-api-key"
OPENAI_ORGANIZATION="your-org-id"

# JWT
JWT_SECRET="your-super-secret-jwt-key"
JWT_REFRESH_SECRET="your-super-secret-refresh-key"

# Server
PORT=4000
NODE_ENV=development

# Frontend
VITE_API_URL="http://localhost:4000"
VITE_APP_NAME="Focus Todo Turbinado"

# Email (opcional)
SMTP_HOST="smtp.gmail.com"
SMTP_PORT=587
SMTP_USER="your-email@gmail.com"
SMTP_PASS="your-app-password"

# Monitoring (opcional)
SENTRY_DSN="your-sentry-dsn"
LOGROCKET_APP_ID="your-logrocket-app-id"
```

## 🏗️ Estrutura do Projeto

```
focus-todo-turbinado/
├── 📁 frontend/                 # Aplicação React
│   ├── 📁 src/
│   │   ├── 📁 components/       # Componentes React
│   │   ├── 📁 pages/           # Páginas da aplicação
│   │   ├── 📁 hooks/           # Custom hooks
│   │   ├── 📁 services/        # Serviços de API
│   │   ├── 📁 stores/          # Gerenciamento de estado
│   │   ├── 📁 types/           # Definições TypeScript
│   │   └── 📁 utils/           # Utilitários
│   ├── 📁 public/              # Arquivos estáticos
│   └── 📁 tests/               # Testes do frontend
├── 📁 backend/                  # API Node.js
│   ├── 📁 src/
│   │   ├── 📁 controllers/     # Controladores de API
│   │   ├── 📁 services/        # Lógica de negócio
│   │   ├── 📁 repositories/    # Acesso a dados
│   │   ├── 📁 middleware/      # Middlewares
│   │   ├── 📁 models/          # Modelos de dados
│   │   ├── 📁 routes/          # Definição de rotas
│   │   └── 📁 utils/           # Utilitários
│   ├── 📁 prisma/              # Schema e migrações
│   └── 📁 tests/               # Testes do backend
├── 📁 docs/                    # Documentação
├── 📁 requirements/            # Requisitos
├── 📁 architecture/           # Arquitetura
├── 📁 prompts/                # Prompts de IA
├── 📁 config/                 # Configurações
└── 📁 testing/                # Estratégias de teste
```

## 🚀 Scripts de Desenvolvimento

### Scripts Principais
```bash
# Desenvolvimento
npm run dev                    # Inicia frontend e backend
npm run dev:frontend          # Apenas frontend
npm run dev:backend           # Apenas backend

# Build
npm run build                 # Build de produção
npm run build:frontend        # Build do frontend
npm run build:backend         # Build do backend

# Testes
npm run test                  # Todos os testes
npm run test:unit             # Testes unitários
npm run test:integration      # Testes de integração
npm run test:e2e              # Testes E2E
npm run test:coverage         # Cobertura de testes

# Qualidade de Código
npm run lint                  # Verificar linting
npm run lint:fix              # Corrigir linting
npm run format                # Formatar código
npm run type-check            # Verificar tipos TypeScript

# Banco de Dados
npm run db:migrate            # Executar migrações
npm run db:seed               # Executar seeds
npm run db:reset              # Resetar banco
npm run db:studio             # Abrir Prisma Studio
```

## 🔧 Configuração de Ferramentas

### ESLint Configuration
```javascript
// .eslintrc.js
module.exports = {
  extends: [
    'eslint:recommended',
    '@typescript-eslint/recommended',
    'plugin:react/recommended',
    'plugin:react-hooks/recommended',
    'plugin:jsx-a11y/recommended'
  ],
  plugins: ['@typescript-eslint', 'react', 'jsx-a11y'],
  rules: {
    '@typescript-eslint/no-unused-vars': 'error',
    'react/react-in-jsx-scope': 'off',
    'react/prop-types': 'off'
  },
  settings: {
    react: {
      version: 'detect'
    }
  }
};
```

### Prettier Configuration
```json
// .prettierrc
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "printWidth": 80,
  "tabWidth": 2,
  "useTabs": false
}
```

### TypeScript Configuration
```json
// tsconfig.json
{
  "compilerOptions": {
    "target": "ES2020",
    "lib": ["dom", "dom.iterable", "es6"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "noFallthroughCasesInSwitch": true,
    "module": "esnext",
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx",
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  },
  "include": ["src"],
  "exclude": ["node_modules"]
}
```

## 🧪 Configuração de Testes

### Jest Setup
```typescript
// tests/setup.ts
import '@testing-library/jest-dom';
import { server } from './mocks/server';

beforeAll(() => server.listen());
afterEach(() => server.resetHandlers());
afterAll(() => server.close());

// Mock IntersectionObserver
global.IntersectionObserver = class IntersectionObserver {
  constructor() {}
  disconnect() {}
  observe() {}
  unobserve() {}
};

// Mock ResizeObserver
global.ResizeObserver = class ResizeObserver {
  constructor() {}
  disconnect() {}
  observe() {}
  unobserve() {}
};
```

### Playwright Setup
```typescript
// tests/e2e/setup/global-setup.ts
import { chromium, FullConfig } from '@playwright/test';

async function globalSetup(config: FullConfig) {
  const browser = await chromium.launch();
  const page = await browser.newPage();
  
  // Setup test data
  await page.goto('http://localhost:3000');
  await page.fill('[data-testid="email-input"]', 'test@example.com');
  await page.fill('[data-testid="password-input"]', 'password123');
  await page.click('[data-testid="login-button"]');
  
  // Store authentication state
  await page.context().storageState({ path: 'tests/e2e/setup/auth.json' });
  await browser.close();
}

export default globalSetup;
```

## 📝 Convenções de Código

### Nomenclatura
```typescript
// Arquivos e pastas
components/          // PascalCase para componentes
user-profile.tsx     // kebab-case para arquivos
useAuth.ts           // camelCase para hooks
TaskService.ts       // PascalCase para classes

// Variáveis e funções
const userName = '';           // camelCase
const API_BASE_URL = '';       // UPPER_SNAKE_CASE
function getUserData() {}      // camelCase
class TaskRepository {}        // PascalCase

// Interfaces e tipos
interface UserProfile {}       // PascalCase
type TaskStatus = '';          // PascalCase
```

### Estrutura de Componentes
```typescript
// components/TaskCard/TaskCard.tsx
import React from 'react';
import { Task } from '@/types/task';
import { TaskCardProps } from './TaskCard.types';
import { useTaskCard } from './useTaskCard';
import './TaskCard.css';

export const TaskCard: React.FC<TaskCardProps> = ({ task, onEdit, onDelete }) => {
  const { handleEdit, handleDelete, isEditing } = useTaskCard({ task, onEdit, onDelete });

  return (
    <div className="task-card" data-testid="task-card">
      <h3>{task.title}</h3>
      <p>{task.description}</p>
      <div className="task-actions">
        <button onClick={handleEdit} data-testid="edit-task-button">
          Edit
        </button>
        <button onClick={handleDelete} data-testid="delete-task-button">
          Delete
        </button>
      </div>
    </div>
  );
};
```

### Estrutura de Serviços
```typescript
// services/TaskService.ts
import { Task, CreateTaskData } from '@/types/task';
import { TaskRepository } from '@/repositories/TaskRepository';
import { OpenAIService } from '@/services/OpenAIService';
import { logger } from '@/utils/logger';

export class TaskService {
  constructor(
    private taskRepository: TaskRepository,
    private openAIService: OpenAIService
  ) {}

  async createTask(data: CreateTaskData): Promise<Task> {
    try {
      logger.info('Creating task', { title: data.title });
      
      const aiAnalysis = await this.openAIService.analyzeTask(data);
      const task = await this.taskRepository.create({
        ...data,
        aiAnalysis
      });

      logger.info('Task created successfully', { taskId: task.id });
      return task;
    } catch (error) {
      logger.error('Failed to create task', { error, data });
      throw error;
    }
  }

  async getTasksByUser(userId: string, filters?: any): Promise<Task[]> {
    try {
      return await this.taskRepository.findByUser(userId, filters);
    } catch (error) {
      logger.error('Failed to get tasks', { error, userId });
      throw error;
    }
  }
}
```

## 🔌 Integração com IA

### Configuração do OpenAI
```typescript
// services/OpenAIService.ts
import OpenAI from 'openai';
import { TaskData, AIAnalysis } from '@/types';
import { logger } from '@/utils/logger';

export class OpenAIService {
  private openai: OpenAI;

  constructor() {
    this.openai = new OpenAI({
      apiKey: process.env.OPENAI_API_KEY,
      organization: process.env.OPENAI_ORGANIZATION
    });
  }

  async analyzeTask(taskData: TaskData): Promise<AIAnalysis> {
    try {
      const prompt = this.buildTaskAnalysisPrompt(taskData);
      
      const response = await this.openai.chat.completions.create({
        model: 'gpt-4',
        messages: [{ role: 'user', content: prompt }],
        temperature: 0.3,
        max_tokens: 1000
      });

      const analysis = this.parseAIResponse(response.choices[0].message.content);
      
      logger.info('AI analysis completed', { 
        taskTitle: taskData.title,
        confidence: analysis.confidence 
      });

      return analysis;
    } catch (error) {
      logger.error('AI analysis failed', { error, taskData });
      throw new Error('Failed to analyze task with AI');
    }
  }

  private buildTaskAnalysisPrompt(taskData: TaskData): string {
    return `
      Analise a seguinte tarefa e forneça:
      1. Prioridade sugerida (baixa, média, alta, urgente)
      2. Tempo estimado em minutos
      3. Sugestões de otimização
      4. Categoria recomendada

      Tarefa: ${taskData.title}
      Descrição: ${taskData.description}
      Prazo: ${taskData.dueDate}
      Categoria: ${taskData.category}

      Responda em JSON válido.
    `;
  }

  private parseAIResponse(content: string): AIAnalysis {
    try {
      return JSON.parse(content);
    } catch (error) {
      logger.error('Failed to parse AI response', { content, error });
      throw new Error('Invalid AI response format');
    }
  }
}
```

## 🗄️ Banco de Dados

### Schema Prisma
```prisma
// prisma/schema.prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

model User {
  id        String   @id @default(cuid())
  email     String   @unique
  password  String
  name      String
  avatarUrl String?
  preferences Json    @default("{}")
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt

  tasks     Task[]
  pomodoroSessions PomodoroSession[]
  analytics ProductivityAnalytics[]

  @@map("users")
}

model Task {
  id            String    @id @default(cuid())
  userId        String
  title         String
  description   String?
  status        TaskStatus @default(PENDING)
  priority      Priority  @default(MEDIUM)
  category      String?
  dueDate       DateTime?
  estimatedTime Int?
  aiAnalysis    Json?
  createdAt     DateTime  @default(now())
  updatedAt     DateTime  @updatedAt

  user          User      @relation(fields: [userId], references: [id], onDelete: Cascade)
  pomodoroSessions PomodoroSession[]

  @@map("tasks")
}

model PomodoroSession {
  id        String   @id @default(cuid())
  userId    String
  taskId    String?
  duration  Int
  completed Boolean  @default(false)
  startedAt DateTime @default(now())
  endedAt   DateTime?

  user      User     @relation(fields: [userId], references: [id], onDelete: Cascade)
  task      Task?    @relation(fields: [taskId], references: [id], onDelete: SetNull)

  @@map("pomodoro_sessions")
}

model ProductivityAnalytics {
  id                String   @id @default(cuid())
  userId            String
  date              DateTime @db.Date
  tasksCompleted    Int      @default(0)
  totalFocusTime    Int      @default(0)
  productivityScore Decimal  @db.Decimal(3, 2)
  aiInsights        Json?
  createdAt         DateTime @default(now())

  user              User     @relation(fields: [userId], references: [id], onDelete: Cascade)

  @@unique([userId, date])
  @@map("productivity_analytics")
}

enum TaskStatus {
  PENDING
  IN_PROGRESS
  COMPLETED
  CANCELLED
}

enum Priority {
  LOW
  MEDIUM
  HIGH
  URGENT
}
```

### Migrações
```bash
# Criar nova migração
npm run db:migrate:create -- --name add_user_preferences

# Executar migrações pendentes
npm run db:migrate

# Reverter última migração
npm run db:migrate:reset

# Verificar status das migrações
npm run db:migrate:status
```

## 🔒 Segurança

### Autenticação JWT
```typescript
// middleware/auth.ts
import jwt from 'jsonwebtoken';
import { Request, Response, NextFunction } from 'express';

export const authenticateJWT = (req: Request, res: Response, next: NextFunction) => {
  const authHeader = req.headers.authorization;

  if (!authHeader) {
    return res.status(401).json({ message: 'No token provided' });
  }

  const token = authHeader.split(' ')[1];

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET!);
    req.user = decoded;
    next();
  } catch (error) {
    return res.status(401).json({ message: 'Invalid token' });
  }
};
```

### Validação de Dados
```typescript
// middleware/validation.ts
import { z } from 'zod';
import { Request, Response, NextFunction } from 'express';

export const validateRequest = (schema: z.ZodSchema) => {
  return (req: Request, res: Response, next: NextFunction) => {
    try {
      schema.parse(req.body);
      next();
    } catch (error) {
      if (error instanceof z.ZodError) {
        return res.status(400).json({
          message: 'Validation failed',
          errors: error.errors
        });
      }
      next(error);
    }
  };
};

// Schemas de validação
export const createTaskSchema = z.object({
  title: z.string().min(1, 'Title is required').max(255),
  description: z.string().optional(),
  category: z.string().optional(),
  dueDate: z.string().datetime().optional(),
  priority: z.enum(['low', 'medium', 'high', 'urgent']).optional()
});
```

## 📊 Monitoramento e Logs

### Configuração de Logs
```typescript
// utils/logger.ts
import winston from 'winston';

const logger = winston.createLogger({
  level: process.env.LOG_LEVEL || 'info',
  format: winston.format.combine(
    winston.format.timestamp(),
    winston.format.errors({ stack: true }),
    winston.format.json()
  ),
  defaultMeta: { service: 'focus-todo-api' },
  transports: [
    new winston.transports.Console({
      format: winston.format.combine(
        winston.format.colorize(),
        winston.format.simple()
      )
    }),
    new winston.transports.File({ 
      filename: 'logs/error.log', 
      level: 'error' 
    }),
    new winston.transports.File({ 
      filename: 'logs/combined.log' 
    })
  ]
});

export { logger };
```

### Métricas de Performance
```typescript
// middleware/metrics.ts
import { Request, Response, NextFunction } from 'express';
import { logger } from '@/utils/logger';

export const performanceMiddleware = (req: Request, res: Response, next: NextFunction) => {
  const start = Date.now();

  res.on('finish', () => {
    const duration = Date.now() - start;
    
    logger.info('Request completed', {
      method: req.method,
      url: req.url,
      statusCode: res.statusCode,
      duration,
      userAgent: req.get('User-Agent')
    });
  });

  next();
};
```

## 🚀 Deploy

### Deploy Frontend (Vercel)
```bash
# Instalar Vercel CLI
npm i -g vercel

# Fazer login
vercel login

# Deploy
vercel --prod
```

### Deploy Backend (Railway)
```bash
# Instalar Railway CLI
npm i -g @railway/cli

# Fazer login
railway login

# Deploy
railway up
```

### Docker Deploy
```bash
# Build das imagens
docker-compose build

# Executar em produção
docker-compose -f docker-compose.prod.yml up -d
```

## 🔄 Workflow de Desenvolvimento

### 1. Criar Feature Branch
```bash
git checkout -b feature/nova-funcionalidade
```

### 2. Desenvolver Feature
```bash
# Fazer alterações no código
# Executar testes
npm run test

# Verificar qualidade
npm run lint
npm run type-check
```

### 3. Commit e Push
```bash
git add .
git commit -m "feat: adiciona nova funcionalidade

- Implementa feature X
- Adiciona testes
- Atualiza documentação"
git push origin feature/nova-funcionalidade
```

### 4. Pull Request
- Criar PR no GitHub
- Revisar código
- Executar CI/CD
- Aprovar e merge

## 📚 Recursos Adicionais

### Documentação
- [React Documentation](https://react.dev/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [Prisma Documentation](https://www.prisma.io/docs/)
- [OpenAI API Documentation](https://platform.openai.com/docs/)

### Ferramentas Úteis
- **VS Code Extensions**: ESLint, Prettier, TypeScript, React DevTools
- **Browser Extensions**: React DevTools, Redux DevTools
- **API Testing**: Postman, Insomnia
- **Database**: pgAdmin, DBeaver

### Comunidade
- **Discord**: Canal do projeto
- **GitHub Issues**: Para bugs e features
- **GitHub Discussions**: Para dúvidas e discussões

## 🆘 Suporte

### Problemas Comuns
1. **Erro de conexão com banco**: Verificar se PostgreSQL está rodando
2. **Erro de Redis**: Verificar se Redis está rodando
3. **Erro de OpenAI**: Verificar API key e créditos
4. **Erro de build**: Limpar cache e node_modules

### Contatos
- **Email**: dev@focus-todo-turbinado.com
- **GitHub Issues**: Para bugs e features
- **Discord**: Para suporte em tempo real

---

**Lembre-se**: Este é um projeto em constante evolução. Mantenha-se atualizado com as últimas mudanças e contribua para melhorar a documentação! 