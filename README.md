## Estrutura do Projeto

PROJECT-ROOT/
├── src/
│   ├── config/         
│   ├── controllers/    
│   ├── middleware/     
│   ├── models/         
│   ├── routes/         
│   ├── services/       
├── server.js           
├── tests/              
├── .env                
├── package.json        
├── README.md          

Documentação da API
Visão Geral
Esta API fornece endpoints para a criação, leitura, atualização e exclusão de categorias e produtos. A API foi desenvolvida utilizando Node.js, Express.js, e Sequelize ORM para interação com o banco de dados MySQL. Autenticação JWT é utilizada para proteger os endpoints que realizam alterações nos dados.

Autenticação
Geração de Token JWT
Endpoint: POST /v1/user/token
Descrição: Gera um token JWT para autenticação.
Headers:
Content-Type: application/json
Corpo da Requisição:json

Copiar código:
{
  "email": "user@mail.com",
  "password": "123@123"
}
Resposta de Sucesso:
Status: 200 OK
Body: json

Copiar código:
{
  "token": "jwt_token_aqui"
}
Códigos de Status:
200 OK: Quando o token é gerado com sucesso.
401 Unauthorized: Quando as credenciais estão incorretas.
Endpoints de Categorias
1. Listar Categorias
Endpoint: GET /v1/category/search
Descrição: Retorna uma lista de categorias com suporte para paginação, filtragem, e seleção de campos.
Parâmetros de Consulta:
limit: Número máximo de itens por página. (-1 para todos os itens, padrão: 12)
page: Página atual. (Padrão: 1)
fields: Campos específicos a serem retornados. (e.g., name,slug)
use_in_menu: Filtra categorias que podem aparecer no menu. (true ou false)
Resposta de Sucesso:
Status: 200 OK
Body: json
Copiar código
{
  "categories": [
{
"id": 1,
      "name": "Categoria 1",
      "slug": "categoria-1",
      "use_in_menu": true
    },
    ...
  ],
  "total": 20,
  "limit": 12,
  "page": 1
}
Códigos de Status:
200 OK: Quando a lista é retornada com sucesso.
3. Obter Categoria por ID
Endpoint: GET /v1/category/:id
Descrição: Retorna os detalhes de uma categoria específica.
Parâmetros de Rota:
id: ID da categoria.
Resposta de Sucesso:
Status: 200 OK
Body:
json
Copiar código
{
  "id": 1,
  "name": "Categoria 1",
  "slug": "categoria-1",
  "use_in_menu": true
}
Códigos de Status:
200 OK: Quando a categoria é encontrada.
404 Not Found: Quando a categoria não é encontrada.
4. Criar Categoria
Endpoint: POST /v1/category
Descrição: Cria uma nova categoria.
Headers:
Content-Type: application/json
Authorization: Bearer {jwt_token}
Corpo da Requisição:
json
Copiar código
{
  "name": "Nova Categoria",
  "slug": "nova-categoria",
  "use_in_menu": true
}
Resposta de Sucesso:
Status: 201 Created
Body:
json
Copiar código
{
  "id": 1,
  "name": "Nova Categoria",
  "slug": "nova-categoria",
  "use_in_menu": true
}
Códigos de Status:
201 Created: Quando a categoria é criada com sucesso.
400 Bad Request: Quando há erros de validação no corpo da requisição.
5. Atualizar Categoria
Endpoint: PUT /v1/category/:id
Descrição: Atualiza uma categoria existente.
Headers:
Content-Type: application/json
Authorization: Bearer {jwt_token}
Parâmetros de Rota:
id: ID da categoria.
Corpo da Requisição:
json
Copiar código
{
  "name": "Categoria Atualizada",
  "slug": "categoria-atualizada",
  "use_in_menu": false
}
Resposta de Sucesso:
Status: 204 No Content
Códigos de Status:
204 No Content: Quando a categoria é atualizada com sucesso.
400 Bad Request: Quando há erros de validação no corpo da requisição.
404 Not Found: Quando a categoria não é encontrada.
6. Deletar Categoria
Endpoint: DELETE /v1/category/:id
Descrição: Remove uma categoria específica.
Headers:
Authorization: Bearer {jwt_token}
Parâmetros de Rota:
id: ID da categoria.
Resposta de Sucesso:
Status: 204 No Content
Códigos de Status:
204 No Content: Quando a categoria é removida com sucesso.
404 Not Found: Quando a categoria não é encontrada.
Endpoints de Produtos
1. Listar Produtos
Endpoint: GET /v1/product/search
Descrição: Retorna uma lista de produtos com suporte para paginação, filtragem, e seleção de campos.
Parâmetros de Consulta:
limit: Número máximo de itens por página. (-1 para todos os itens, padrão: 12)
page: Página atual. (Padrão: 1)
fields: Campos específicos a serem retornados. (e.g., name,price,images)
match: Termo para busca por nome ou descrição do produto.
category_ids: Filtra produtos pelos IDs das categorias.
price-range: Faixa de preço para filtragem (e.g., 100-200).
option[id]: Filtra produtos pelos valores das opções.
Resposta de Sucesso:
Status: 200 OK
Body:
json
Copiar código
{
  "products": [
    {
      "id": 1,
      "name": "Produto 1",
      "price": 99.90,
      "images": [
        {
          "id": 1,
          "content": "https://store.com/media/product-01/image-01.png"
        }
      ],
      ...
    },
    ...
  ],
  "total": 50,
  "limit": 12,
  "page": 1
}
Códigos de Status:
200 OK: Quando a lista é retornada com sucesso.
2. Obter Produto por ID
Endpoint: GET /v1/product/:id
Descrição: Retorna os detalhes de um produto específico.
Parâmetros de Rota:
id: ID do produto.
Resposta de Sucesso:
Status: 200 OK
Body:
json
Copiar código
{
  "id": 1,
  "name": "Produto 1",
  "price": 99.90,
  "description": "Descrição do produto 1",
  "stock": 10,
  "images": [
    {
      "id": 1,
      "content": "https://store.com/media/product-01/image-01.png"
    }
  ],
  "options": [
    {
      "id": 1,
      "title": "Cor",
      "values": ["Vermelho", "Azul"]
    }
  ],
  ...
}
Códigos de Status:
200 OK: Quando o produto é encontrado.
404 Not Found: Quando o produto não é encontrado.
3. Criar Produto
Endpoint: POST /v1/product
Descrição: Cria um novo produto.
Headers:
Content-Type: application/json
Authorization: Bearer {jwt_token}
Corpo da Requisição:
json
Copiar código
{
  "name": "Novo Produto",
  "slug": "novo-produto",
  "price": 199.90,
  "price_with_discount": 149.90,
  "stock": 50,
  "description": "Descrição do novo produto",
  "category_ids": [1, 2],
  "images": [
    {
      "type": "image/png",
      "content": "base64 da imagem 1"
    }
  ],
  "options": [
    {
      "title": "Cor",
      "values": ["Preto", "Branco"]
    }
  ]
}
Resposta de Sucesso:
Status: 201 Created
Body:
json
Copiar código
{
  "id": 1,
  "name": "Novo Produto",
  "slug": "novo-produto",
  ...
}
Códigos de Status:
201 Created: Quando o produto é criado com sucesso.
400 Bad Request: Quando há erros de validação no corpo da requisição.
4. Atualizar Produto
Endpoint: PUT /v1/product/:id
Descrição: Atualiza um produto existente.
Headers:
Content-Type: application/json
Authorization: Bearer {jwt_token}
Parâmetros de Rota:
id: ID do produto.
Corpo da Requisição:
json
Copiar código
{
  "name": "Produto Atualizado",
  "slug": "produto-atualizado",
  "price": 149.90,
  "price_with_discount": 129.90,
  "stock": 30,
  "description": "Descrição atualizada do produto",
  "category_ids": [1, 2],
  "images": [
    {
      "type": "image/png",
      "content": "base64 da imagem atualizada"
    }
  ],
  "options": [
    {
      "title": "Tamanho",
      "values": ["P", "M", "G"]
    }
  ]
}
Resposta de Sucesso:
Status: 204 No Content
Códigos de Status:
204 No Content: Quando o produto é atualizado com sucesso.
400 Bad Request: Quando há erros de validação no corpo da requisição.
404 Not Found: Quando o produto não é encontrado.
5. Deletar Produto
Endpoint: DELETE /v1/product/:id
Descrição: Remove um produto específico.
Headers:
Authorization: Bearer {jwt_token}
Parâmetros de Rota:
id: ID do produto.
Resposta de Sucesso:
Status: 204 No Content
Códigos de Status:
204 No Content: Quando o produto é removido com sucesso.
404 Not Found: Quando o produto não é encontrado.
