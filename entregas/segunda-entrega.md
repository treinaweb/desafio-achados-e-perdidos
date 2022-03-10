# Segunda Entrega

## Descrição

Durante essa entrega você terá que desenvolver as rotas e telas referentes as funcionalidades de gerenciamento de objetos e listagem de objetos por local.

## Requisitos Funcionais

Os requisitos funcionais que estão relacionados com essa entrega são:

- **RAP02 - Listar objetos do local**: O administrador do departamento de achados e perdidos poderá realizar a listagem dos objetos cadastrados para o local.

- **RAP03 - Cadastrar objeto para o local**: O administrador do departamento de achados e perdidos poderá realizar o cadastro de um objeto para o local.

- **RAP04 - Editar informações do objeto**: O administrador do departamento de achados e perdidos poderá realizar a edição das informações de um objeto previamente cadastrado para o local.

- **RAP05 - Excluir objeto**: O administrador do departamento de achados e perdidos poderá realizar a exclusão de um objeto previamente cadastrado para o local.

## RAP02 - Listar objetos do local

Abaixo você encontrará todas as informações do quê e como deve ser desenvolvido no back-end e no front-end para o caso de uso RAP02.

## Back-end

### Rotas

| Rota                    | Verbo HTTP | Descrição                                                                         |
|-------------------------|------------|-----------------------------------------------------------------------------------|
| /api/objetos            | GET        | Rota responsável por listar os objetos cadastrados para o local do usuário logado |

### Rota GET /api/objetos

**Dados no cabeçalho da requisição**

| Chave         | Tipo   | Exemplo                                                                                                                                                                                                                                                                                                                                                                      |
|---------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authorization | string | Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDU4NTksImV4cCI6MTY0MjQ0OTQ1OSwibmJmIjoxNjQyNDQ1ODU5LCJqdGkiOiJJdFV1QzA5Q1VGQ0JoTDdpIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.CjMddVkovYEawKXNwuMroajTKb52R4X3dC5NvH1ClW0 |

**Dados no corpo da requisição**

Não se aplica

**Dados da resposta**

Dados do objeto

| Campo         | Tipo     | Exemplo                                                                    |
|---------------|----------|----------------------------------------------------------------------------|
| id            | int      | 1                                                                          |
| nome          | string   | Guarda Chuva                                                               |
| descricao     | string   | Cor preta                                                                  |
| entregue      | boolean  | false                                                                      |
| data_cadastro | string   | 2022-01-01                                                                 |
| imagem        | string   | http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png |

Hateoas do Objeto

| Type   | Rel                   | Uri                            |
|------- |-----------------------|--------------------------------|
| GET    | self                  | /api/objetos/{objetoId}        |
| PUT    | atualizar_objeto      | /api/objetos/{objetoId}        |
| DELETE | apagar_objeto         | /api/objetos/{objetoId}        |
| POST   | definir_imagem_objeto | /api/objetos/{objetoId}/imagem |
| PATCH  | definir_dono_objeto   | /api/objetos/{objetoId}/donos  |

**Exemplo de requisição**

```
GET /api/objetos HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*
```

**Exemplos de respostas**

Token válido

```
HTTP/1.1 200 OK
Content-Type: application/json

[
  {
    "id": 1,
    "nome": "Guarda Chuva",
    "descricao": "Cor preta",
    "entregue": false,
    "data_cadastro": "2022-01-01",
    "imagem": "http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png",
    "links": [
      {
        "type": "GET",
        "rel": "self",
        "uri": "/api/objetos/1"
      },
      {
        "type": "PUT",
        "rel": "atualizar_objeto",
        "uri": "/api/objetos/1"
      },
      {
        "type": "DELETE",
        "rel": "apagar_objeto",
        "uri": "/api/objetos/1"
      },
      {
        "type": "POST",
        "rel": "definir_imagem_objeto",
        "uri": "/api/objetos/1/imagem"
      },
      {
        "type": "PATCH",
        "rel": "definir_dono_objeto",
        "uri": "/api/objetos/1/donos"
      }
    ]
  }
]
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

## Front-end

## Telas

Para esse caso de uso a tela à ser desenvolvida é a tela de listagem de objetos.

### Tela de listagem de objetos

Essa tela deve conter uma tabela com o objetos do local pertencente ao usuário logado, para cada objeto deve ser exibido os botões para realizar as ações de "Editar", "Apagar", e "Informar Entrega".

![Tela de listagem dos objetos](../telas/tela-lista-de-objetos.png)

## RAP03 - Cadastrar objeto para o local

Abaixo você encontrará todas as informações do quê e como deve ser desenvolvido no back-end e no front-end para o caso de uso RAP03.

## Back-end

### Rotas

| Rota                            | Verbo HTTP | Descrição                                                          |
|---------------------------------|------------|--------------------------------------------------------------------|
| /api/objetos                    | POST       | Rota responsável por cadastrar um objeto o local do usuário logado |
| /api/objetos/{objetoId}/imagem  | POST       | Rota responsável por atualizar a foto de um objeto                 |

### Rota POST /api/objetos

**Dados no cabeçalho da requisição**

| Chave         | Tipo   | Exemplo                                                                                                                                                                                                                                                                                                                                                                      |
|---------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authorization | string | Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDU4NTksImV4cCI6MTY0MjQ0OTQ1OSwibmJmIjoxNjQyNDQ1ODU5LCJqdGkiOiJJdFV1QzA5Q1VGQ0JoTDdpIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.CjMddVkovYEawKXNwuMroajTKb52R4X3dC5NvH1ClW0 |

**Dados no corpo da requisição**

| Campo     | Tipo   | Exemplo      |
|---------- |--------|--------------|
| nome      | string | Guarda Chuva |
| descricao | string | Cor preta    |

Regras de validação do objeto:

- `nome`: não pode ser nulo
- `nome`: não pode ser vazio
- `nome`: não pode ser menor que 3 caracteres
- `nome`: não pode ser maior que 255 caracteres
- `descricao`: não pode ser nulo
- `descricao`: não pode ser vazio
- `descricao`: não pode ser menor que 3 caracteres
- `descricao`: não pode ser maior que 255 caracteres

**Dados da resposta**

Dados do Objeto

| Campo         | Tipo    | Exemplo                                                                    |
|---------------|-------- |----------------------------------------------------------------------------|
| id            | int     | 1                                                                          |
| nome          | string  | Guarda Chuva                                                               |
| descricao     | string  | Cor preta                                                                  |
| entregue      | boolean | false                                                                      |
| data_cadastro | string  | 2022-01-01                                                                 |
| imagem        | string  | http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png |

Hateos do Objeto

| Type   | Rel                   | Uri                            |
|------- |-----------------------|--------------------------------|
| GET    | self                  | /api/objetos/{objetoId}        |
| PUT    | atualizar_objeto      | /api/objetos/{objetoId}        |
| DELETE | apagar_objeto         | /api/objetos/{objetoId}        |
| POST   | definir_imagem_objeto | /api/objetos/{objetoId}/imagem |
| PATCH  | definir_dono_objeto   | /api/objetos/{objetoId}/donos  |

**Exemplo de requisição**

```
POST /api/objetos HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*

{
	"nome": "Guarda Chuva",
	"descricao": "Cor preta"
}
```

**Exemplos de respostas**

Dados válidos

```
HTTP/1.1 201 OK
Content-Type: application/json

{
  "id": 1,
  "nome": "Guarda Chuva",
  "descricao": "Cor preta",
  "entregue": false,
  "data_cadastro": "2022-01-01",
  "imagem": "http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png",
  "links": [
    {
      "type": "GET",
      "rel": "self",
      "uri": "/api/objetos/1"
    },
    {
      "type": "PUT",
      "rel": "atualizar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "DELETE",
      "rel": "apagar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "POST",
      "rel": "definir_imagem_objeto",
      "uri": "/api/objetos/1/imagem"
    },
    {
      "type": "PATCH",
      "rel": "definir_dono_objeto",
      "uri": "/api/objetos/1/donos"
    }
  ]
}
```

Dados inválidos

```
HTTP/1.1 400
Content-Type: application/json

{
  "status": 400,
  "code": "validation_error",
  "message": "Erro de validação dos dados enviados",
  "nome": [
    "O campo nome é obrigatório."
  ]
}
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

### Rota POST /api/objetos/{objetoId}/imagem

**Dados no cabeçalho da requisição**

| Chave         | Tipo   | Exemplo                                                                                                                                                                                                                                                                                                                                                                      |
|---------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authorization | string | Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDU4NTksImV4cCI6MTY0MjQ0OTQ1OSwibmJmIjoxNjQyNDQ1ODU5LCJqdGkiOiJJdFV1QzA5Q1VGQ0JoTDdpIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.CjMddVkovYEawKXNwuMroajTKb52R4X3dC5NvH1ClW0 |

**Dados no corpo da requisição**

| Campo         | Tipo   | Exemplo |
|---------------|--------|---------|
| imagem_objeto | file   | -       |

Regras de validação:

- `imagem_objeto`: não pode ser nulo
- `imagem_objeto`: deve ser uma imagem

**Dados da resposta**

| Campo    | Tipo   | Exemplo                      |
|----------|--------|------------------------------|
| mensagem | string | Imagem definida com sucesso! |

**Exemplo de requisição**

```
POST /api/objetos/1/imagem HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*
```

**Exemplos de respostas**

Dados válidos:

```
HTTP/1.1 200
Content-Type: application/json

{
  "message": "Imagem definida com sucesso!"
}
```

Dados inválidos:

```
HTTP/1.1 400
Content-Type: application/json

{
  "status": 400,
  "code": "validation_error",
  "message": "Erro de validação dos dados enviados",
  "imagem_local": [
    "O campo imagem local é obrigatório."
  ]
}
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

Objeto não encontrado

```
HTTP/1.1 404
Content-Type: application/json

{
  "message": "Objeto não encontrado"
}
```

## Front-end

## Telas

Para esse caso de uso a tela à ser desenvolvida é a tela com o formulário de um objeto.

### Tela de formulário do objeto

Essa tela será utilizada para o cadastro de um objeto, ela deve conter um formulario para que se possa informar os dados do objeto a ser cadastrado.

![Tela de formulário do objeto](../telas/tela-cadastrar-objeto.png)

## RAP04 - Editar informações do objeto

Abaixo você encontrará todas as informações do quê e como deve ser desenvolvido no back-end e no front-end para o caso de uso RAP04.

## Back-end

### Rotas

| Rota                    | Verbo HTTP | Descrição                                         |
|-------------------------|------------|---------------------------------------------------|
| /api/objetos/{objetoId} | GET        | Rota responsável por exibir os dados de um objeto |
| /api/objetos/{objetoId} | PUT        | Rota responsável por alterar dados de um objeto   |

### Rota GET /api/objetos/{objetoId}

**Dados no cabeçalho da requisição**

| Chave         | Tipo   | Exemplo                                                                                                                                                                                                                                                                                                                                                                      |
|---------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authorization | string | Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDU4NTksImV4cCI6MTY0MjQ0OTQ1OSwibmJmIjoxNjQyNDQ1ODU5LCJqdGkiOiJJdFV1QzA5Q1VGQ0JoTDdpIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.CjMddVkovYEawKXNwuMroajTKb52R4X3dC5NvH1ClW0 |

**Dados no corpo da requisição**

Não se aplica

**Dados da resposta**

Dados do Objeto

| Campo         | Tipo    | Exemplo                                                                    |
|---------------|-------- |----------------------------------------------------------------------------|
| id            | int     | 1                                                                          |
| nome          | string  | Guarda Chuva                                                               |
| descricao     | string  | Cor preta                                                                  |
| entregue      | boolean | false                                                                      |
| data_cadastro | string  | 2022-01-01                                                                 |
| imagem        | string  | http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png |

Hateoas do Objeto

| Type   | Rel                   | Uri                            |
|------- |-----------------------|--------------------------------|
| GET    | self                  | /api/objetos/{objetoId}        |
| PUT    | atualizar_objeto      | /api/objetos/{objetoId}        |
| DELETE | apagar_objeto         | /api/objetos/{objetoId}        |
| POST   | definir_imagem_objeto | /api/objetos/{objetoId}/imagem |
| PATCH  | definir_dono_objeto   | /api/objetos/{objetoId}/donos  |

**Exemplo de requisição**

```
GET /api/objetos/1 HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*
```

**Exemplos de respostas**

Dados válidos

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "nome": "Guarda Chuva",
  "descricao": "Cor preta",
  "entregue": false,
  "data_cadastro": "2022-01-01",
  "imagem": "http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png",
  "links": [
    {
      "type": "GET",
      "rel": "self",
      "uri": "/api/objetos/1"
    },
    {
      "type": "PUT",
      "rel": "atualizar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "DELETE",
      "rel": "apagar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "POST",
      "rel": "definir_imagem_objeto",
      "uri": "/api/objetos/1/imagem"
    },
    {
      "type": "PATCH",
      "rel": "definir_dono_objeto",
      "uri": "/api/objetos/1/donos"
    }
  ]
}
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

Objeto não encontrado

```
HTTP/1.1 404
Content-Type: application/json

{
  "message": "Objeto não encontrado"
}
```

### Rota PUT /api/objetos/{objetoId}

**Dados no cabeçalho da requisição**

| Chave         | Tipo   | Exemplo                                                                                                                                                                                                                                                                                                                                                                      |
|---------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authorization | string | Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDU4NTksImV4cCI6MTY0MjQ0OTQ1OSwibmJmIjoxNjQyNDQ1ODU5LCJqdGkiOiJJdFV1QzA5Q1VGQ0JoTDdpIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.CjMddVkovYEawKXNwuMroajTKb52R4X3dC5NvH1ClW0 |

**Dados no corpo da requisição**

| Campo     | Tipo   | Exemplo      |
|---------- |--------|--------------|
| nome      | string | Guarda Chuva |
| descricao | string | Cor preta    |

Regras de validação do objeto:

- `nome`: não pode ser nulo
- `nome`: não pode ser vazio
- `nome`: não pode ser menor que 3 caracteres
- `nome`: não pode ser maior que 255 caracteres
- `descricao`: não pode ser nulo
- `descricao`: não pode ser vazio
- `descricao`: não pode ser menor que 3 caracteres
- `descricao`: não pode ser maior que 255 caracteres

**Dados da resposta**

Dados do Objeto

| Campo         | Tipo    | Exemplo                                                                    |
|---------------|-------- |----------------------------------------------------------------------------|
| id            | int     | 1                                                                          |
| nome          | string  | Guarda Chuva                                                               |
| descricao     | string  | Cor preta                                                                  |
| entregue      | boolean | false                                                                      |
| data_cadastro | string  | 2022-01-01                                                                 |
| imagem        | string  | http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png |

Hateoas do Objeto

| Type   | Rel                   | Uri                            |
|------- |-----------------------|--------------------------------|
| GET    | self                  | /api/objetos/{objetoId}        |
| PUT    | atualizar_objeto      | /api/objetos/{objetoId}        |
| DELETE | apagar_objeto         | /api/objetos/{objetoId}        |
| POST   | definir_imagem_objeto | /api/objetos/{objetoId}/imagem |
| PATCH  | definir_dono_objeto   | /api/objetos/{objetoId}/donos  |

**Exemplo de requisição**

```
PUT /api/objetos/1 HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*

{
	"nome": "Guarda Chuva",
	"descricao": "Cor preta"
}
```

**Exemplos de respostas**

Dados válidos

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "nome": "Guarda Chuva",
  "descricao": "Cor preta",
  "entregue": false,
  "data_cadastro": "2022-01-01",
  "imagem": "http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png",
  "links": [
    {
      "type": "GET",
      "rel": "self",
      "uri": "/api/objetos/1"
    },
    {
      "type": "PUT",
      "rel": "atualizar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "DELETE",
      "rel": "apagar_objeto",
      "uri": "/api/objetos/1"
    },
    {
      "type": "POST",
      "rel": "definir_imagem_objeto",
      "uri": "/api/objetos/1/imagem"
    },
    {
      "type": "PATCH",
      "rel": "definir_dono_objeto",
      "uri": "/api/objetos/1/donos"
    }
  ]
}
```

Dados inválidos

```
HTTP/1.1 400
Content-Type: application/json

{
  "status": 400,
  "code": "validation_error",
  "message": "Erro de validação dos dados enviados",
  "nome": [
    "O campo nome é obrigatório."
  ]
}
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

Objeto não encontrado

```
HTTP/1.1 404
Content-Type: application/json

{
  "message": "Objeto não encontrado"
}
```

## Front-end

## Telas

Para esse caso de uso sera feito um reaproveitamento da tela de formulário de objetos, com a diferença que na edição o formulario já deve vir preenchido com os dados do objeto que está sendo editado.

## RAP05 - Excluir objeto

Abaixo você encontrará todas as informações do quê e como deve ser desenvolvido no back-end e no front-end para o caso de uso RAP05.

## Back-end

### Rotas

| Rota                    | Verbo HTTP | Descrição                              |
|-------------------------|------------|----------------------------------------|
| /api/objetos/{objetoId} | DELETE     | Rota responsável por excluir um objeto |

### Rota DELETE /api/objetos/{objetoId}

**Dados no cabeçalho da requisição**

| Chave         | Tipo   | Exemplo                                                                                                                                                                                                                                                                                                                                                                      |
|---------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authorization | string | Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDU4NTksImV4cCI6MTY0MjQ0OTQ1OSwibmJmIjoxNjQyNDQ1ODU5LCJqdGkiOiJJdFV1QzA5Q1VGQ0JoTDdpIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.CjMddVkovYEawKXNwuMroajTKb52R4X3dC5NvH1ClW0 |

**Dados no corpo da requisição**

Não se aplica

**Dados da resposta**

Não se aplica

**Exemplo de requisição**

```
DELETE /api/objetos/1 HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDk1OTMsImV4cCI6MTY0MjQ1MzE5MywibmJmIjoxNjQyNDQ5NTkzLCJqdGkiOiJJelhZWHlYQ2ZkanJHV2xmIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.d7G7gx_aIrnQh1WS9T9BNiHN0ObCxmRhWnqb0tQ6w4s
Accept: */*
```

**Exemplos de respostas**

Dados válidos

```
HTTP/1.1 204 OK
```

Token inválido

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Token inválido"
}
```

Objeto não encontrado

```
HTTP/1.1 404
Content-Type: application/json

{
  "message": "Objeto não encontrado"
}
```

## Front-end

## Telas

Para esse caso de uso não será necessário o desenvolvimento de nenhuma tela, pois a funcionalidade será executada a partir do botão excluir localizado na tela de listagem dos objetos.
