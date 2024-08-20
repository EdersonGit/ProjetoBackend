# Geração Tech - Projeto Back-end

Este é o projeto back-end desenvolvido como parte do curso **Desenvolvedor Web Fullstack** do projeto **Geração Tech** da Digital College.

## Tecnologias Utilizadas

- Node.js
- JavaScript
- Express
- MySQL
- Sequelize
- JsonWebToken (JWT)
- dotenv
- bcrypt
- Git
- GitHub

## Estrutura de Diretórios

```plaintext
├── src/
│   ├── config/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── services/
│   ├── app.js
│   └── server.js
├── .env
├── .gitignore
├── package.json
└── README.md
```

## Configuração do Ambiente

1. Clone o repositório:

    ```bash
    git clone https://github.com/EdersonGit/ProjetoBackend.git
    ```

2. Navegue até o diretório do projeto:

    ```bash
    cd project-root
    ```

3. Configuração do Banco de Dados:

Este projeto utiliza o MySQL como banco de dados. Crie um banco de dados no MySQL e configure as credenciais no arquivo .env:

    ```bash
    DB_HOST=localhost
    DB_USER=seu_usuario
    DB_PASSWORD=sua_senha
    DB_NAME=nome_do_banco_de_dados
    ```


## Endpoints da API

### Endpoints de Usuários

<details>
  <summary> Criar Usuário</summary>

  - **POST** `/v1/user`
    - **Headers**:
      - `Content-type: application/json`
      - `Authorization: Bearer <JWT>`
    - **Payload**:
      ```json
      {
        "firstname": "user firstname",
        "surname": "user surname",
        "email": "user@mail.com",
        "password": "123@123",
        "confirmPassword": "123@123"
      }
      ```
    - **Response Status Code**:
      - `201 Created`: Cadastro bem-sucedido.
      - `400 Bad Request`: Dados incorretos na requisição.

</details>

<details>
  <summary> Buscar Usuário por ID</summary>

- **GET** `/v1/user/:id`
  - **Response Body**:
    ```json
    {
      "id": 1,
      "firstname": "user firstname",
      "surname": "user surname",
      "email": "user@mail.com"
    }
    ```
  - **Response Status Code**:
    - `200 OK`: Requisição bem-sucedida.
    - `404 Not Found`: Usuário não encontrado.
<details>

<details>
  <summary> Atualizar Usuário</summary>

- **PUT** `/v1/user/:id`
  - **Headers**:
    - `Content-type: application/json`
    - `Authorization: Bearer <JWT>`
  - **Payload**:
    ```json
    {
      "firstname": "user firstname",
      "surname": "user surname",
      "email": "user@mail.com"
    }
    ```
  - **Response Status Code**:
    - `204 No Content`: Atualização bem-sucedida, sem conteúdo de resposta.
    - `400 Bad Request`: Dados incorretos na requisição.
    - `401 Unauthorized`: Token de autorização não enviado ou incorreto.
    - `404 Not Found`: Usuário não encontrado.
<details>

<details>
  <summary> Deletar Usuário</summary>

- **DELETE** `/v1/user/:id`
  - **Headers**:
    - `Content-type: application/json`
    - `Authorization: Bearer <JWT>`
  - **Response Status Code**:
    - `204 No Content`: Exclusão bem-sucedida, sem conteúdo de resposta.
    - `401 Unauthorized`: Token de autorização não enviado ou incorreto.
    - `404 Not Found`: Usuário não encontrado.
<details>

### Endpoints de Categorias

<details>
  <summary> Listar Categorias </summary>

- **GET** `/v1/category/search`
  - **Query Params**:
    - `limit=-1`: Limite de itens por página. Use `-1` para buscar todos os itens (padrão: 12).
    - `page=1`: Página dos dados retornados (padrão: 1).
    - `fields=name,slug`: Limita os campos retornados.
    - `use_in_menu=true`: Filtra categorias que podem aparecer no menu.
  - **Response Body**:
    ```json
    {
      "data": [
        {
          "id": 1,
          "name": "Shoes",
          "slug": "shoes",
          "use_in_menu": true
        },
        {
          "id": 2,
          "name": "Offers",
          "slug": "offers",
          "use_in_menu": true
        },
        {
          "id": 3,
          "name": "Black Friday",
          "slug": "black-friday",
          "use_in_menu": false
        }
      ],
      "total": 10,
      "limit": -1,
      "page": 1
    }
    ```
  - **Response Status Code**:
    - `200 OK`: Requisição bem-sucedida.
    - `400 Bad Request`: Dados incorretos na requisição.
<details>

<details>
  <summary> Buscar Categoria por ID </summary>

- **GET** `/v1/category/:id`
  - **Response Body**:
    ```json
    {
      "id": 1,
      "name": "Shoes",
      "slug": "shoes",
      "use_in_menu": true
    }
    ```
  - **Response Status Code**:
    - `200 OK`: Requisição bem-sucedida.
    - `404 Not Found`: Categoria não encontrada.
<details>

<details>
  <summary> Criar Categoria </summary>

- **POST** `/v1/category`
  - **Headers**:
    - `Content-type: application/json`
    - `Authorization: Bearer <JWT>`
  - **Payload**:
    ```json
    {
      "name": "Shoes",
      "slug": "shoes",
      "use_in_menu": true
    }
    ```
  - **Response Status Code**:
    - `201 Created`: Cadastro bem-sucedido.
    - `400 Bad Request`: Dados incorretos na requisição.
    - `401 Unauthorized`: Token de autorização não enviado ou incorreto.
<details>

<details>
  <summary> Atualizar Categoria </summary>

- **PUT** `/v1/category/:id`
  - **Headers**:
    - `Content-type: application/json`
    - `Authorization: Bearer <JWT>`
  - **Payload**:
    ```json
    {
      "name": "Shoes",
      "slug": "shoes",
      "use_in_menu": true
    }
    ```
  - **Response Status Code**:
    - `204 No Content`: Atualização bem-sucedida, sem conteúdo de resposta.
    - `400 Bad Request`: Dados incorretos na requisição.
    - `401 Unauthorized`: Token de autorização não enviado ou incorreto.
    - `404 Not Found`: Categoria não encontrada.
<details>

<details>
  <summary> Deletar Categoria </summary>

- **DELETE** `/v1/category/:id`
  - **Headers**:
    - `Content-type: application/json`
    - `Authorization: Bearer <JWT>`
  - **Response Status Code**:
    - `204 No Content`: Exclusão bem-sucedida, sem conteúdo de resposta.
    - `401 Unauthorized`: Token de autorização não enviado ou incorreto.
    - `404 Not Found`: Categoria não encontrada.
<details>

### Endpoints de Produtos

<details>
  <summary> Listar Produtos </summary>

- **GET** `/v1/product/search`
  - **Query Params**:
    - `limit=30`: Limite de itens por página. Use `-1` para buscar todos os itens (padrão: 12).
    - `page=2`: Página dos dados retornados (padrão: 1).
    - `fields=name,images,price`: Limita os campos retornados.
    - `match=Tênis`: Filtra por termo que combine com o nome ou descrição.
    - `category_ids=15,24`: Filtra pelo ID das categorias.
    - `price-range=100-200`: Filtra por faixa de preços.
    - `option[45]=GG,PP`: Filtra pelo valor das opções disponíveis.
  - **Response Body**:
    ```json
    {
      "data": [
        {
          "id": 1,
          "enabled": true,
          "name": "Produto 01",
          "slug": "produto-01",
          "stock": 10,
          "description": "Descrição do produto 01",
          "price": 119.90,
          "price_with_discount": 99.90,
          "category_ids": [{"id": 1}, {"id": 15}, {"id": 24}, {"id": 68}],
          "images": [
            {
              "id": 1,
              "path": "https://store.com/media/product-01/image-01.png"
            },
            {
              "id": 2,
              "path": "https://store.com/media/product-01/image-02.png"
            },
            {
              "id": 3,
              "path": "https://store.com/media/product-01/image-02.jpg"
            }
          ],
          "options": [
            { 
              "id": 1,
              "title": "Cor",
              "values": ["PP", "GG"]
            },
            { 
              "id": 2,
              "title": "Tamanho",
              "values": ["P", "M", "G"]
            }
          ]
        }
      ],
      "total": 120,
      "limit": 12,
      "page": 1
    }
    ```
  - **Response Status Code**:
    - `200 OK`: Requisição bem-sucedida.
    - `400 Bad Request`: Dados incorretos na requisição.
<details>

<details>
  <summary> Buscar Produto por ID </summary>

- **GET** `/v1/product/:id`
  - **Response Body**:
    ```json
    {
      "id": 1,
      "enabled": true,
      "name": "Produto 01",
      "slug": "produto-01",
      "stock": 10,
      "description": "Descrição do produto 01",
      "price": 119.90,
      "price_with_discount": 99.90,
      "category_ids": [1],
      "images": [
        {
          "id": 1,
          "path": "https://store.com/media/product-01/image-01.png"
        },
        {
          "id": 2,
          "path": "https://store.com/media/product-01/image-02.png"
        },
        {
          "id": 3,
          "path": "https://store.com/media/product-01/image-02.jpg"
        }
      ],
      "options": [
        { 
          "id": 1,
          "title": "Cor",
          "values": ["PP", "GG"]
        },
        { 
          "id": 2,
          "title": "Tamanho",
          "values": ["P", "M", "G"]
        }
      ]
    }
    ```
  - **Response Status Code**:
    - `200 OK`: Requisição bem-sucedida.
    - `404 Not Found`: Produto não encontrado.
<details>

<details>
  <summary> Criar Produto </summary>

- **POST** `/v1/product`
  - **Headers**:
    - `Content-type: application/json`
    - `Authorization: Bearer <JWT>`
  - **Payload**:
    ```json
      {
    "enabled": true,
    "name": "Produto 01",
    "slug": "produto-01",
    "stock": 10,
    "description": "Descrição do produto 01",
    "price": 119.90,
    "price_with_discount": 99.90,
    "category_ids": [1, 15, 24, 68],
    "images": [ 
      {
        "type": "image/png",
        "content": "base64 da imagem 1" 
      },
      {
        "type": "image/png",
        "content": "base64 da imagem 2" 
      },
      {
        "type": "image/jpg",
        "content": "base64 da imagem 3" 
      }
    ],
    "options": [
      {
        "title": "Cor",
        "shape": "square",
        "radius": "4",
        "type": "text",
        "values": ["PP", "GG", "M"]
      },
      {
        "title": "Tamanho",
        "shape": "circle",
        "type": "color",
        "values": ["#000", "#333"]
      }
    ]
  }
    ```
  - **Response Status Code**:
    - `201 Created`: Cadastro bem-sucedido.
    - `400 Bad Request`: Dados incorretos na requisição.
    - `401 Unauthorized`: Token de autorização não enviado ou incorreto.
<details>

<details>
  <summary> Atualizar Produto </summary>

- **PUT** `/v1/product/:id`
  - **Headers**:
    - `Content-type: application/json`
    - `Authorization: Bearer <JWT>`
  - **Payload**:
    ```json
     {
    "enabled": true,
    "name": "Produto 01 atualizado",
    "slug": "produto-01-atualizado",
    "stock": 20,
    "description": "Descrição do produto 01 atualizado",
    "price": 49.9,
    "price_with_discount": 0,
    "category_ids": [1, 15, 24, 68],
    "images": [ 
      {
        "type": "image/png",
        "content": "base64 da imagem 1" 
      },
      {
        "id": 2,
        "deleted": true
      },
      {
        "id": 3,
        "content": "base64 da imagem 3" 
      },
      {
        "id": 1,
        "content": "https://store.com/media/product-01/image-01.jpg"
      }
    ],
    "options": [
      {
        "id": 1,
        "deleted": true
      },
      {
        "id": 2,
        "radius": "10px",
        "values": ["42/43", "44/45"]
      },
      {
        "title": "Tipo",
        "shape": "square",
        "type": "text",
        "values": ["100% algodão", "65% algodão"]
      }
    ]
  }
    ```
  - **Response Status Code**:
    - `204 No Content`: Atualização bem-sucedida, sem conteúdo de resposta.
    - `400 Bad Request`: Dados incorretos na requisição.
    - `401 Unauthorized`: Token de autorização não enviado ou incorreto.
    - `404 Not Found`: Produto não encontrado.
<details>

<details>
  <summary> Deletar Produto </summary>

- **DELETE** `/v1/product/:id`
  - **Headers**:
    - `Content-type: application/json`
    - `Authorization: Bearer <JWT>`
  - **Response Status Code**:
    - `204 No Content`: Exclusão bem-sucedida, sem conteúdo de resposta.
    - `401 Unauthorized`: Token de autorização não enviado ou incorreto.
    - `404 Not Found`: Produto não encontrado.
<details>

## Gerar Token

<details>
  <summary> Deletar Produto </summary>

-**Endpoint:** `POST /v1/user/token`
-**Headers:**
- `Content-type: application/json`
- `Authorization: Bearer <JWT>`
**Payload:**
```json
{
  "email": "user@mail.com",
  "password": "123@123"
}
```
**Response Body**:
```json
Copiar código
{
  "token": "<JWT>"
}
```
- **Response Status Code**:
    - `200 OK`: Retornado quando a requisição foi bem-sucedida..
    - `400 Bad Request`: Retornado quando a os dados da requisição estiverem incorretos.
<details>
