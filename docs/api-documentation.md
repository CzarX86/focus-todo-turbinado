# 📚 Documentação da API - Focus Todo Turbinado

## 🎯 Visão Geral

A API do Focus Todo Turbinado é uma API RESTful que fornece endpoints para gerenciamento de tarefas, autenticação de usuários, integração com IA e funcionalidades de produtividade.

**Base URL**: `https://api.focus-todo-turbinado.railway.app`  
**Versão**: v1  
**Formato**: JSON  

## 🔐 Autenticação

A API utiliza JWT (JSON Web Tokens) para autenticação. Todos os endpoints protegidos requerem o header `Authorization` com o formato:

```
Authorization: Bearer <token>
```

### Tipos de Token
- **Access Token**: Válido por 15 minutos
- **Refresh Token**: Válido por 7 dias

## 📋 Endpoints

### 🔑 Autenticação

#### POST /api/auth/register
Registra um novo usuário.

**Request Body:**
```json
{
  "name": "João Silva",
  "email": "joao@exemplo.com",
  "password": "senha123"
}
```

**Response (201):**
```json
{
  "user": {
    "id": "user_123",
    "name": "João Silva",
    "email": "joao@exemplo.com",
    "createdAt": "2024-01-15T10:30:00Z"
  },
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

#### POST /api/auth/login
Autentica um usuário existente.

**Request Body:**
```json
{
  "email": "joao@exemplo.com",
  "password": "senha123"
}
```

**Response (200):**
```json
{
  "user": {
    "id": "user_123",
    "name": "João Silva",
    "email": "joao@exemplo.com"
  },
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

#### POST /api/auth/refresh
Renova o access token usando o refresh token.

**Request Body:**
```json
{
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Response (200):**
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

#### POST /api/auth/logout
Invalida o refresh token.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Request Body:**
```json
{
  "refreshToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Response (200):**
```json
{
  "message": "Logged out successfully"
}
```

### 📝 Tarefas

#### GET /api/tasks
Lista todas as tarefas do usuário autenticado.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Query Parameters:**
- `status` (optional): `pending`, `in_progress`, `completed`, `cancelled`
- `priority` (optional): `low`, `medium`, `high`, `urgent`
- `category` (optional): string
- `search` (optional): string para busca por título
- `page` (optional): número da página (default: 1)
- `limit` (optional): itens por página (default: 20)

**Response (200):**
```json
{
  "tasks": [
    {
      "id": "task_123",
      "title": "Implementar autenticação",
      "description": "Criar sistema de login com JWT",
      "status": "pending",
      "priority": "high",
      "category": "development",
      "dueDate": "2024-01-20T23:59:59Z",
      "estimatedTime": 120,
      "aiAnalysis": {
        "suggestedPriority": "high",
        "estimatedTime": 120,
        "optimizationSuggestions": ["Break into smaller tasks"],
        "confidence": 0.85
      },
      "createdAt": "2024-01-15T10:30:00Z",
      "updatedAt": "2024-01-15T10:30:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 1,
    "totalPages": 1
  }
}
```

#### POST /api/tasks
Cria uma nova tarefa com análise de IA opcional.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Request Body:**
```json
{
  "title": "Implementar autenticação",
  "description": "Criar sistema de login com JWT",
  "category": "development",
  "dueDate": "2024-01-20T23:59:59Z",
  "priority": "high",
  "enableAI": true
}
```

**Response (201):**
```json
{
  "id": "task_123",
  "title": "Implementar autenticação",
  "description": "Criar sistema de login com JWT",
  "status": "pending",
  "priority": "high",
  "category": "development",
  "dueDate": "2024-01-20T23:59:59Z",
  "estimatedTime": 120,
  "aiAnalysis": {
    "suggestedPriority": "high",
    "estimatedTime": 120,
    "optimizationSuggestions": ["Break into smaller tasks"],
    "recommendedCategory": "development",
    "confidence": 0.85,
    "reasoning": "This is a critical security feature that should be prioritized"
  },
  "createdAt": "2024-01-15T10:30:00Z",
  "updatedAt": "2024-01-15T10:30:00Z"
}
```

#### GET /api/tasks/:id
Obtém detalhes de uma tarefa específica.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Response (200):**
```json
{
  "id": "task_123",
  "title": "Implementar autenticação",
  "description": "Criar sistema de login com JWT",
  "status": "pending",
  "priority": "high",
  "category": "development",
  "dueDate": "2024-01-20T23:59:59Z",
  "estimatedTime": 120,
  "aiAnalysis": {
    "suggestedPriority": "high",
    "estimatedTime": 120,
    "optimizationSuggestions": ["Break into smaller tasks"],
    "confidence": 0.85
  },
  "pomodoroSessions": [
    {
      "id": "session_123",
      "duration": 25,
      "completed": true,
      "startedAt": "2024-01-15T10:00:00Z",
      "endedAt": "2024-01-15T10:25:00Z"
    }
  ],
  "createdAt": "2024-01-15T10:30:00Z",
  "updatedAt": "2024-01-15T10:30:00Z"
}
```

#### PUT /api/tasks/:id
Atualiza uma tarefa existente.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Request Body:**
```json
{
  "title": "Implementar autenticação JWT",
  "description": "Criar sistema de login com JWT e refresh tokens",
  "status": "in_progress",
  "priority": "urgent",
  "category": "development",
  "dueDate": "2024-01-18T23:59:59Z"
}
```

**Response (200):**
```json
{
  "id": "task_123",
  "title": "Implementar autenticação JWT",
  "description": "Criar sistema de login com JWT e refresh tokens",
  "status": "in_progress",
  "priority": "urgent",
  "category": "development",
  "dueDate": "2024-01-18T23:59:59Z",
  "updatedAt": "2024-01-15T11:00:00Z"
}
```

#### DELETE /api/tasks/:id
Remove uma tarefa.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Response (204):**
```
No Content
```

#### POST /api/tasks/:id/analyze
Reanalisa uma tarefa com IA.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Response (200):**
```json
{
  "aiAnalysis": {
    "suggestedPriority": "urgent",
    "estimatedTime": 90,
    "optimizationSuggestions": [
      "Use existing authentication libraries",
      "Implement proper error handling",
      "Add comprehensive tests"
    ],
    "recommendedCategory": "security",
    "confidence": 0.92,
    "reasoning": "Authentication is critical for security and should be prioritized"
  }
}
```

### 🍅 Pomodoro

#### POST /api/pomodoro/start
Inicia uma sessão Pomodoro.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Request Body:**
```json
{
  "taskId": "task_123",
  "duration": 25
}
```

**Response (201):**
```json
{
  "id": "session_123",
  "taskId": "task_123",
  "duration": 25,
  "startedAt": "2024-01-15T10:00:00Z",
  "estimatedEndAt": "2024-01-15T10:25:00Z"
}
```

#### PUT /api/pomodoro/:id/pause
Pausa uma sessão Pomodoro.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Response (200):**
```json
{
  "id": "session_123",
  "status": "paused",
  "pausedAt": "2024-01-15T10:15:00Z",
  "remainingTime": 600
}
```

#### PUT /api/pomodoro/:id/resume
Retoma uma sessão Pomodoro pausada.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Response (200):**
```json
{
  "id": "session_123",
  "status": "active",
  "resumedAt": "2024-01-15T10:20:00Z",
  "estimatedEndAt": "2024-01-15T10:30:00Z"
}
```

#### PUT /api/pomodoro/:id/complete
Finaliza uma sessão Pomodoro.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Response (200):**
```json
{
  "id": "session_123",
  "status": "completed",
  "completedAt": "2024-01-15T10:25:00Z",
  "totalDuration": 25
}
```

#### GET /api/pomodoro/sessions
Lista sessões Pomodoro do usuário.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Query Parameters:**
- `taskId` (optional): ID da tarefa
- `status` (optional): `active`, `paused`, `completed`
- `date` (optional): Data específica (YYYY-MM-DD)
- `page` (optional): número da página
- `limit` (optional): itens por página

**Response (200):**
```json
{
  "sessions": [
    {
      "id": "session_123",
      "taskId": "task_123",
      "taskTitle": "Implementar autenticação",
      "duration": 25,
      "status": "completed",
      "startedAt": "2024-01-15T10:00:00Z",
      "completedAt": "2024-01-15T10:25:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 20,
    "total": 1,
    "totalPages": 1
  }
}
```

### 📊 Analytics

#### GET /api/analytics/productivity
Obtém insights de produtividade do usuário.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Query Parameters:**
- `period` (optional): `day`, `week`, `month` (default: `week`)
- `startDate` (optional): Data inicial (YYYY-MM-DD)
- `endDate` (optional): Data final (YYYY-MM-DD)

**Response (200):**
```json
{
  "period": "week",
  "startDate": "2024-01-08",
  "endDate": "2024-01-14",
  "summary": {
    "totalTasks": 15,
    "completedTasks": 12,
    "completionRate": 0.8,
    "totalFocusTime": 1800,
    "averageSessionLength": 25,
    "productivityScore": 85.5
  },
  "dailyStats": [
    {
      "date": "2024-01-08",
      "tasksCompleted": 2,
      "focusTime": 300,
      "productivityScore": 82.3
    }
  ],
  "aiInsights": {
    "overallScore": 85.5,
    "strengths": [
      "Consistent daily work routine",
      "Good task completion rate"
    ],
    "weaknesses": [
      "Could improve time estimation",
      "Consider shorter breaks between sessions"
    ],
    "recommendations": [
      {
        "type": "optimization",
        "description": "Try 20-minute sessions instead of 25",
        "impact": "medium",
        "implementation": "Adjust Pomodoro timer settings"
      }
    ],
    "nextWeekGoals": {
      "targetTasks": 18,
      "focusHours": 20,
      "priorityAreas": ["time_management", "task_prioritization"]
    }
  }
}
```

#### GET /api/analytics/patterns
Obtém análise de padrões de trabalho.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Response (200):**
```json
{
  "workPatterns": {
    "optimalWorkHours": ["09:00", "11:00", "14:00", "16:00"],
    "recommendedSessionLength": 25,
    "breakStrategy": "5-minute breaks between sessions, 15-minute break every 4 sessions",
    "productivityPeaks": ["10:00", "15:00"]
  },
  "categoryAnalysis": {
    "mostProductiveCategory": "development",
    "categoryBreakdown": [
      {
        "category": "development",
        "tasksCompleted": 8,
        "averageTime": 120,
        "productivityScore": 88.5
      }
    ]
  },
  "scheduleRecommendations": {
    "morningRoutine": [
      "Review daily tasks",
      "Start with high-priority development tasks"
    ],
    "afternoonFocus": [
      "Continue with medium-priority tasks",
      "Schedule meetings and collaboration"
    ],
    "eveningWrapup": [
      "Complete pending tasks",
      "Plan for tomorrow"
    ]
  }
}
```

### 🤖 IA

#### POST /api/ai/analyze-task
Analisa uma tarefa com IA sem salvá-la.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Request Body:**
```json
{
  "title": "Implementar sistema de notificações",
  "description": "Criar sistema de notificações push para o app",
  "category": "development",
  "dueDate": "2024-01-25T23:59:59Z"
}
```

**Response (200):**
```json
{
  "analysis": {
    "suggestedPriority": "medium",
    "estimatedTime": 180,
    "optimizationSuggestions": [
      "Use existing notification libraries",
      "Implement progressive enhancement",
      "Add user preferences for notifications"
    ],
    "recommendedCategory": "development",
    "confidence": 0.78,
    "reasoning": "Notifications are important for user engagement but not critical for core functionality"
  }
}
```

#### POST /api/ai/analyze-productivity
Analisa dados de produtividade com IA.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Request Body:**
```json
{
  "period": "week",
  "data": {
    "tasksCompleted": 12,
    "totalFocusTime": 1800,
    "averageSessionLength": 25,
    "productivityScore": 85.5
  }
}
```

**Response (200):**
```json
{
  "insights": {
    "overallScore": 85.5,
    "trend": "improving",
    "strengths": [
      "Consistent work routine",
      "Good task completion rate"
    ],
    "weaknesses": [
      "Could improve time estimation"
    ],
    "recommendations": [
      {
        "type": "optimization",
        "description": "Use AI suggestions for time estimation",
        "impact": "high",
        "implementation": "Enable AI analysis for all new tasks"
      }
    ]
  }
}
```

### 👤 Usuário

#### GET /api/user/profile
Obtém perfil do usuário autenticado.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Response (200):**
```json
{
  "id": "user_123",
  "name": "João Silva",
  "email": "joao@exemplo.com",
  "avatarUrl": "https://example.com/avatar.jpg",
  "preferences": {
    "theme": "dark",
    "pomodoroDuration": 25,
    "breakDuration": 5,
    "notifications": true
  },
  "stats": {
    "totalTasks": 45,
    "completedTasks": 38,
    "totalFocusTime": 5400,
    "streak": 7
  },
  "createdAt": "2024-01-01T00:00:00Z",
  "updatedAt": "2024-01-15T10:30:00Z"
}
```

#### PUT /api/user/profile
Atualiza perfil do usuário.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Request Body:**
```json
{
  "name": "João Silva Santos",
  "preferences": {
    "theme": "light",
    "pomodoroDuration": 30,
    "breakDuration": 10,
    "notifications": false
  }
}
```

**Response (200):**
```json
{
  "id": "user_123",
  "name": "João Silva Santos",
  "email": "joao@exemplo.com",
  "preferences": {
    "theme": "light",
    "pomodoroDuration": 30,
    "breakDuration": 10,
    "notifications": false
  },
  "updatedAt": "2024-01-15T11:00:00Z"
}
```

#### POST /api/user/change-password
Altera senha do usuário.

**Headers:**
```
Authorization: Bearer <access_token>
```

**Request Body:**
```json
{
  "currentPassword": "senha123",
  "newPassword": "novaSenha456"
}
```

**Response (200):**
```json
{
  "message": "Password changed successfully"
}
```

## 📊 Códigos de Status

| Código | Descrição |
|--------|-----------|
| 200 | OK - Requisição bem-sucedida |
| 201 | Created - Recurso criado com sucesso |
| 204 | No Content - Requisição bem-sucedida sem conteúdo |
| 400 | Bad Request - Dados inválidos |
| 401 | Unauthorized - Token inválido ou ausente |
| 403 | Forbidden - Acesso negado |
| 404 | Not Found - Recurso não encontrado |
| 422 | Unprocessable Entity - Validação falhou |
| 429 | Too Many Requests - Rate limit excedido |
| 500 | Internal Server Error - Erro interno do servidor |

## 🔄 Rate Limiting

A API implementa rate limiting para proteger contra abuso:

- **Limite geral**: 100 requests por 15 minutos por IP
- **Endpoints de autenticação**: 10 requests por 15 minutos por IP
- **Endpoints de IA**: 60 requests por hora por usuário

**Headers de resposta:**
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1642248600
```

## 🚨 Tratamento de Erros

### Formato de Erro
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Validation failed",
    "details": [
      {
        "field": "email",
        "message": "Invalid email format"
      }
    ]
  }
}
```

### Códigos de Erro Comuns

| Código | Descrição |
|--------|-----------|
| `VALIDATION_ERROR` | Erro de validação de dados |
| `AUTHENTICATION_ERROR` | Erro de autenticação |
| `AUTHORIZATION_ERROR` | Erro de autorização |
| `NOT_FOUND` | Recurso não encontrado |
| `RATE_LIMIT_EXCEEDED` | Rate limit excedido |
| `AI_SERVICE_ERROR` | Erro no serviço de IA |
| `DATABASE_ERROR` | Erro no banco de dados |

## 📝 Exemplos de Uso

### Exemplo Completo: Criar Tarefa com IA
```bash
# 1. Login
curl -X POST https://api.focus-todo-turbinado.railway.app/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "joao@exemplo.com",
    "password": "senha123"
  }'

# Response: {"accessToken": "eyJ..."}

# 2. Criar tarefa com IA
curl -X POST https://api.focus-todo-turbinado.railway.app/api/tasks \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer eyJ..." \
  -d '{
    "title": "Implementar sistema de notificações",
    "description": "Criar sistema de notificações push para o app",
    "category": "development",
    "enableAI": true
  }'

# 3. Iniciar Pomodoro
curl -X POST https://api.focus-todo-turbinado.railway.app/api/pomodoro/start \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer eyJ..." \
  -d '{
    "taskId": "task_123",
    "duration": 25
  }'
```

### Exemplo com JavaScript
```javascript
const API_BASE = 'https://api.focus-todo-turbinado.railway.app';

class FocusTodoAPI {
  constructor(token) {
    this.token = token;
  }

  async createTask(taskData) {
    const response = await fetch(`${API_BASE}/api/tasks`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${this.token}`
      },
      body: JSON.stringify(taskData)
    });

    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }

    return response.json();
  }

  async getTasks(filters = {}) {
    const params = new URLSearchParams(filters);
    const response = await fetch(`${API_BASE}/api/tasks?${params}`, {
      headers: {
        'Authorization': `Bearer ${this.token}`
      }
    });

    return response.json();
  }

  async startPomodoro(taskId, duration = 25) {
    const response = await fetch(`${API_BASE}/api/pomodoro/start`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${this.token}`
      },
      body: JSON.stringify({ taskId, duration })
    });

    return response.json();
  }
}

// Uso
const api = new FocusTodoAPI('your-access-token');

// Criar tarefa
const task = await api.createTask({
  title: 'Implementar autenticação',
  description: 'Criar sistema de login com JWT',
  category: 'development',
  enableAI: true
});

// Listar tarefas
const tasks = await api.getTasks({ status: 'pending' });

// Iniciar Pomodoro
const session = await api.startPomodoro(task.id, 25);
```

## 🔗 Webhooks

A API suporta webhooks para notificações em tempo real:

### Configurar Webhook
```bash
curl -X POST https://api.focus-todo-turbinado.railway.app/api/webhooks \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer eyJ..." \
  -d '{
    "url": "https://your-app.com/webhook",
    "events": ["task.created", "pomodoro.completed"]
  }'
```

### Eventos Disponíveis
- `task.created` - Nova tarefa criada
- `task.updated` - Tarefa atualizada
- `task.completed` - Tarefa concluída
- `pomodoro.started` - Sessão Pomodoro iniciada
- `pomodoro.completed` - Sessão Pomodoro concluída

## 📈 Monitoramento

### Health Check
```bash
curl https://api.focus-todo-turbinado.railway.app/health
```

**Response:**
```json
{
  "status": "healthy",
  "timestamp": "2024-01-15T10:30:00Z",
  "services": {
    "database": "connected",
    "redis": "connected",
    "openai": "connected"
  },
  "version": "1.0.0"
}
```

### Métricas
```bash
curl https://api.focus-todo-turbinado.railway.app/metrics
```

## 🔄 Versionamento

A API segue versionamento semântico. Para acessar versões específicas:

- **v1 (atual)**: `https://api.focus-todo-turbinado.railway.app/api/v1/`
- **v2 (futuro)**: `https://api.focus-todo-turbinado.railway.app/api/v2/`

## 📞 Suporte

- **Documentação**: [docs.focus-todo-turbinado.com](https://docs.focus-todo-turbinado.com)
- **Status**: [status.focus-todo-turbinado.com](https://status.focus-todo-turbinado.com)
- **Email**: api-support@focus-todo-turbinado.com
- **GitHub Issues**: [github.com/focus-todo-turbinado/api/issues](https://github.com/focus-todo-turbinado/api/issues)

---

**Última atualização**: 15 de Janeiro de 2024  
**Versão da API**: 1.0.0 