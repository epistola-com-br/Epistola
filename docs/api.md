# 🔗 API Documentation - Epístola

Esta documentação descreve as APIs da plataforma Epístola. Todas as APIs seguem padrões REST e retornam JSON.

## 🌍 Base URLs

- **Production**: `https://api.epistola.com.br`
- **Staging**: `https://api-staging.epistola.com.br`
- **Development**: `http://localhost:3000`

## 🔐 Autenticação

### Bearer Token
```bash
curl -H "Authorization: Bearer YOUR_TOKEN" \
     https://api.epistola.com.br/v1/users/me
```

### API Key (para Epistolários)
```bash
curl -H "X-API-Key: YOUR_API_KEY" \
     -H "X-Client-ID: YOUR_CLIENT_ID" \
     https://api.epistola.com.br/v1/oauth/authorize
```

## 📋 Convenções

### HTTP Status Codes
- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `422` - Validation Error
- `429` - Rate Limited
- `500` - Internal Server Error

### Response Format
```json
{
  "success": true,
  "data": { ... },
  "meta": {
    "timestamp": "2024-01-01T12:00:00Z",
    "request_id": "req_123456"
  }
}
```

### Error Format
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": [
      {
        "field": "email",
        "message": "Email is required"
      }
    ]
  },
  "meta": {
    "timestamp": "2024-01-01T12:00:00Z",
    "request_id": "req_123456"
  }
}
```

---

## 👤 Authentication API

### POST /v1/auth/register
Registra um novo usuário

**Request:**
```json
{
  "email": "user@example.com",
  "username": "johndoe",
  "password": "securepassword123",
  "accept_terms": true
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "user": {
      "id": 123,
      "email": "user@example.com",
      "username": "johndoe",
      "email_verified": false,
      "created_at": "2024-01-01T12:00:00Z"
    },
    "tokens": {
      "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9...",
      "refresh_token": "rt_abcd1234...",
      "expires_in": 3600
    }
  }
}
```

### POST /v1/auth/login
Autentica um usuário

**Request:**
```json
{
  "email": "user@example.com",
  "password": "securepassword123"
}
```

### POST /v1/auth/refresh
Renova access token

**Request:**
```json
{
  "refresh_token": "rt_abcd1234..."
}
```

### POST /v1/auth/logout
Invalida tokens do usuário

### POST /v1/auth/forgot-password
Solicita recuperação de senha

**Request:**
```json
{
  "email": "user@example.com"
}
```

---

## 🏢 OAuth API (para Epistolários)

### POST /v1/oauth/authorize
Gera URL de autorização para Epistolário

**Headers:**
```
X-API-Key: your_api_key
X-Client-ID: your_client_id
```

**Request:**
```json
{
  "permissions": ["read:profile", "read:inventory"],
  "redirect_uri": "https://meuepistolario.com/callback",
  "state": "random_state_string"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "authorization_url": "https://auth.epistola.com.br/authorize?client_id=...&state=...",
    "expires_in": 600
  }
}
```

### POST /v1/oauth/token
Troca authorization code por access token

**Request:**
```json
{
  "client_id": "your_client_id",
  "client_secret": "your_client_secret",
  "code": "auth_code_from_callback",
  "grant_type": "authorization_code"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "access_token": "at_user_token...",
    "token_type": "Bearer",
    "expires_in": 3600,
    "scope": "read:profile read:inventory",
    "user_id": 123
  }
}
```

---

## 👥 Users API

### GET /v1/users/me
Retorna perfil do usuário autenticado

**Response:**
```json
{
  "success": true,
  "data": {
    "id": 123,
    "email": "user@example.com",
    "username": "johndoe",
    "display_name": "John Doe",
    "avatar_url": "https://cdn.epistola.com.br/avatars/123.jpg",
    "email_verified": true,
    "created_at": "2024-01-01T12:00:00Z",
    "updated_at": "2024-01-01T12:00:00Z"
  }
}
```

### PUT /v1/users/me
Atualiza perfil do usuário

**Request:**
```json
{
  "display_name": "John Doe Updated",
  "bio": "Colecionador de cartas digitais"
}
```

### GET /v1/users/{id}
Retorna perfil público de um usuário

---

## 💰 Wallets API

### GET /v1/wallets/me
Retorna carteira do usuário autenticado

**Response:**
```json
{
  "success": true,
  "data": {
    "user_id": 123,
    "balance": "150.00",
    "locked_balance": "25.00",
    "currency": "SELO",
    "updated_at": "2024-01-01T12:00:00Z"
  }
}
```

### GET /v1/wallets/me/transactions
Lista transações da carteira

**Query Parameters:**
- `page` (int): Página (default: 1)
- `limit` (int): Itens por página (default: 20, max: 100)
- `type` (string): Filtro por tipo (transfer, purchase, refund)
- `status` (string): Filtro por status (pending, completed, failed)

**Response:**
```json
{
  "success": true,
  "data": {
    "transactions": [
      {
        "id": "tx_123456",
        "type": "purchase",
        "amount": "-10.00",
        "status": "completed",
        "description": "Compra de Missiva: Carta Rara #001",
        "created_at": "2024-01-01T12:00:00Z"
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 20,
      "total": 45,
      "pages": 3
    }
  }
}
```

---

## 📜 Missivas API

### GET /v1/missivas
Lista missivas disponíveis

**Query Parameters:**
- `epistolario_id` (int): Filtro por Epistolário
- `category` (string): Filtro por categoria
- `rarity` (string): Filtro por raridade
- `min_price` (decimal): Preço mínimo
- `max_price` (decimal): Preço máximo
- `page` (int): Página
- `limit` (int): Itens por página

**Response:**
```json
{
  "success": true,
  "data": {
    "missivas": [
      {
        "id": 1001,
        "title": "Carta do Explorador",
        "description": "Uma carta lendária dos primeiros exploradores",
        "image_url": "https://cdn.epistola.com.br/missivas/1001.jpg",
        "price": "25.00",
        "rarity": "rare",
        "attributes": {
          "attack": 15,
          "defense": 10,
          "element": "fire"
        },
        "epistolario": {
          "id": 1,
          "name": "Reino dos Dragões",
          "creator": "dragonsmaster"
        },
        "supply": {
          "max": 100,
          "current": 23,
          "available": 77
        },
        "created_at": "2024-01-01T12:00:00Z"
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 20,
      "total": 156,
      "pages": 8
    }
  }
}
```

### GET /v1/missivas/{id}
Retorna detalhes de uma missiva específica

### POST /v1/missivas
Cria nova missiva (apenas criadores de Epistolários)

**Request:**
```json
{
  "title": "Nova Carta Épica",
  "description": "Descrição da carta",
  "price": "15.00",
  "rarity": "epic",
  "max_supply": 50,
  "attributes": {
    "power": 20,
    "speed": 8
  },
  "category": "warriors"
}
```

---

## 🎒 Inventory API

### GET /v1/inventory/me
Retorna inventário do usuário autenticado

**Query Parameters:**
- `epistolario_id` (int): Filtro por Epistolário
- `rarity` (string): Filtro por raridade
- `page` (int): Página

**Response:**
```json
{
  "success": true,
  "data": {
    "items": [
      {
        "id": 5001,
        "missiva": {
          "id": 1001,
          "title": "Carta do Explorador",
          "image_url": "https://cdn.epistola.com.br/missivas/1001.jpg",
          "rarity": "rare"
        },
        "quantity": 2,
        "acquired_at": "2024-01-01T12:00:00Z"
      }
    ],
    "stats": {
      "total_items": 45,
      "total_value": "1250.00",
      "rarities": {
        "common": 20,
        "rare": 15,
        "epic": 8,
        "legendary": 2
      }
    }
  }
}
```

### POST /v1/inventory/transfer
Transfere missiva para outro usuário

**Request:**
```json
{
  "missiva_id": 1001,
  "to_user_id": 456,
  "quantity": 1,
  "message": "Presente para você!"
}
```

---

## 🏪 Shop API

### POST /v1/shop/purchase
Compra missivas

**Request:**
```json
{
  "items": [
    {
      "missiva_id": 1001,
      "quantity": 2
    }
  ]
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "order_id": "order_123456",
    "total_amount": "50.00",
    "items_purchased": 2,
    "transaction_id": "tx_789012"
  }
}
```

### GET /v1/shop/cart
Retorna carrinho do usuário

### POST /v1/shop/cart/add
Adiciona item ao carrinho

---

## 🏛️ Epistolarios API

### GET /v1/epistolarios
Lista Epistolários públicos

**Response:**
```json
{
  "success": true,
  "data": {
    "epistolarios": [
      {
        "id": 1,
        "name": "Reino dos Dragões",
        "description": "Um mundo épico de dragões e magia",
        "logo_url": "https://cdn.epistola.com.br/logos/1.jpg",
        "banner_url": "https://cdn.epistola.com.br/banners/1.jpg",
        "creator": {
          "id": 789,
          "username": "dragonsmaster",
          "display_name": "Dragons Master"
        },
        "stats": {
          "total_missivas": 156,
          "total_sales": "12500.00",
          "active_users": 1250
        },
        "created_at": "2024-01-01T12:00:00Z"
      }
    ]
  }
}
```

### GET /v1/epistolarios/{id}
Detalhes de um Epistolário específico

### POST /v1/epistolarios
Cria novo Epistolário

**Request:**
```json
{
  "name": "Meu Epistolário",
  "description": "Descrição do meu mundo de cartas",
  "category": "fantasy",
  "permissions": ["read:profile", "read:inventory"]
}
```

---

## 📊 Analytics API

### GET /v1/analytics/dashboard
Dashboard analítico para criadores

**Response:**
```json
{
  "success": true,
  "data": {
    "sales": {
      "today": "125.00",
      "this_week": "850.00",
      "this_month": "3200.00",
      "total": "15600.00"
    },
    "missivas": {
      "total": 45,
      "published": 42,
      "draft": 3
    },
    "users": {
      "total": 1250,
      "active_today": 89,
      "new_this_week": 23
    }
  }
}
```

---

## ⚡ Rate Limiting

### Limites por Endpoint
- **Auth endpoints**: 5 requests/min per IP
- **Read endpoints**: 100 requests/min per user
- **Write endpoints**: 30 requests/min per user
- **Upload endpoints**: 10 requests/min per user

### Headers de Rate Limit
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640995200
```

---

## 🔔 Webhooks

### Configuração
```json
{
  "url": "https://meuepistolario.com/webhooks",
  "events": ["missiva.purchased", "user.registered"],
  "secret": "webhook_secret_key"
}
```

### Eventos Disponíveis
- `user.registered` - Novo usuário registrado
- `missiva.purchased` - Missiva comprada
- `transaction.completed` - Transação concluída
- `inventory.updated` - Inventário atualizado

### Formato do Webhook
```json
{
  "event": "missiva.purchased",
  "data": {
    "user_id": 123,
    "missiva_id": 1001,
    "quantity": 2,
    "total_price": "50.00",
    "transaction_id": "tx_789012"
  },
  "timestamp": "2024-01-01T12:00:00Z",
  "signature": "sha256=..."
}
```

---

## 🧪 Testing

### Sandbox Environment
Use `https://api-sandbox.epistola.com.br` para testes

### Test Data
```json
{
  "test_user": {
    "email": "test@epistola.com.br",
    "password": "test123456"
  },
  "test_client": {
    "client_id": "test_client_123",
    "client_secret": "test_secret_456"
  }
}
```

---

## 📚 SDKs

### JavaScript/Node.js
```bash
npm install @epistola/sdk
```

```javascript
import { Epistola } from '@epistola/sdk';

const client = new Epistola({
  apiKey: 'your_api_key',
  environment: 'production' // or 'sandbox'
});

const user = await client.users.me();
```

### Python
```bash
pip install epistola-sdk
```

```python
from epistola import Epistola

client = Epistola(
    api_key='your_api_key',
    environment='production'
)

user = client.users.me()
```

---

*Para mais informações, consulte nossa [documentação interativa](https://docs.epistola.com.br) ou entre em contato através do [Discord](https://discord.gg/epistola).*