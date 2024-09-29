# API de Cartas

## 1. Cartas

Todas as cartas estão salvas no arquivo `cards.json` e servem para montar baralhos.

**Endpoint para obter os cards:**

- **URL:** `/cards`
- **Método:** `GET`
- **Descrição:** Retorna uma lista dos 100 cards disponíveis.

### Exemplo:

`GET /cards`

---

## 2. Autenticação & Autorização

A API usa **JWT (JSON Web Tokens)** para autenticação. Apenas usuários logados podem criar e editar seus próprios baralhos.

**Rota para registro de usuário:**

- **URL:** `/register`
- **Método:** `POST`
- **Descrição:** Cria um novo usuário.

### Exemplo:

```plaintext
POST /register
{
  "username": "novoUsuario",
  "password": "senhaForte"
}
```

**Rota de login:**

- **URL:** `/login`
- **Método:** `POST`
- **Descrição:** Gera um token JWT para autenticar as futuras requisições.

### Exemplo:

```plaintext
POST /login
{
  "username": "usuarioExistente",
  "password": "senhaForte"
}
```

Resposta de sucesso:

```plaintext
{
  "token": "seu-token-jwt"
}
```

---

## 3. Baralhos

Os baralhos têm um comandante e 99 cartas. Só o criador pode editá-los.

**Endpoint para criar baralho:**

- **URL:** `/decks`
- **Método:** `POST`
- **Autenticação:** Necessária (JWT)
- **Descrição:** Cria um baralho para o usuário logado.

### Exemplo:

```plaintext
POST /decks
Authorization: Bearer <seu-token-jwt>
{
  "commanderId": "id-do-comandante",
  "cardIds": ["id-carta1", "id-carta2", "...", "id-carta99"]
}
```

---

## 4. Middleware de Autorização

As rotas protegidas exigem o token JWT no cabeçalho da requisição para verificar se o usuário logado tem permissão para modificar o baralho.

### Cabeçalho de exemplo:

```plaintext
Authorization: Bearer <seu-token-jwt>
```

---

## 5. Testes

Para garantir o bom funcionamento da API, execute os testes com:

```plaintext
npm test
```

Isso verifica as regras de negócio, endpoints e a segurança da API.