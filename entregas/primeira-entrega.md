# Primeira Entrega

## Descrição

Durante essa entrega você terá que desenvolver as rotas e telas referentes as funcionalidades de cadastro de usuário e login na aplicação.

## Requisitos Funcionais

Os requisitos funcionais que estão relacionados com essa entrega são:

- **RAP01 - Cadastrar local**: O administrador do departamento de achados e perdidos poderá realizar o cadastro do local na plataforma. O sistema deve permitir que ele entre com os dados do local e os dados de acesso à plataforma.

- **RAP07 - Realizar login**: O administrador do departamento de achados e perdidos poderá realizar login na plataforma. Após o login ele deve ser direcionado para a lista de objetos.

## RAP01 - Cadastrar local

Abaixo você encontrará todas as informações do quê e como deve ser desenvolvido no back-end e no front-end para o caso de uso RAP01.

## Back-end

### Rotas

| Rota               | Verbo HTTP | Descrição                                                                     |
|--------------------|------------|-------------------------------------------------------------------------------|
| /api/locais        | POST       | Rota responsável por cadastrar um novo usuário e um novo local                |
| /api/locais/imagem | POST       | Rota responsável por atualizar a imagem do local pertecente ao usuário logado |

### Rota POST /api/locais

**Dados da requisição**

Dados do local:

| Campo     | Tipo    | Exemplo                            |
|-----------|---------|------------------------------------|
| nome      | string  | Padaria do Sabor                   |
| endereco  | string  | av jardim japao, 98 - Centro - SBC |
| contato   | string  | Whats: 11 99712-3550               |
| descricao | string  | Padaria do bairro                  |
| usuario   | Usuario | -                                  |

Regras de validação do local:

- `nome`: não pode ser nulo
- `nome`: não pode ser vazio
- `nome`: não pode ser menor que 3 caracteres
- `nome`: não pode ser maior que 255 caracteres
- `endereco`: não pode ser nulo
- `endereco`: não pode ser vazio
- `endereco`: não pode ser menor que 3 caracteres
- `endereco`: não pode ser maior que 255 caracteres
- `contato`: não pode ser nulo
- `contato`: não pode ser vazio
- `contato`: não pode ser menor que 3 caracteres
- `contato`: não pode ser maior que 255 caracteres
- `descricao`: não pode ser maior que 255 caracteres
- `usuario`: deve seguir a regras de validação internas do usuário

Dados do usuário:

| Campo                 | Tipo   | Exemplo       |
|-----------------------|--------|---------------|
| nome                  | srting | João da Silva |
| email                 | srting | joao@mail.com |
| passaword             | srting | senha@123     |
| password_confirmation | srting | senha@123     |

Regras de validação do usuário:

- `nome`: não pode ser nulo
- `nome`: não pode ser vazio
- `nome`: não pode ser menor que 3 caracteres
- `nome`: não pode ser maior que 255 caracteres
- `email`: não pode ser nulo
- `email`: não pode ser vazio
- `email`: não pode ser menor que 3 caracteres
- `email`: não pode ser maior que 255 caracteres
- `email`: deve ser um endereço de email válido
- `email`: deve ser único no banco de dados
- `password`: não pode ser nulo
- `password`: não pode ser vazio
- `password_confirmation`: não pode ser nulo
- `password_confirmation`: não pode ser vazio
- `password_confirmation`: deve ser igual ao campo `password`

**Dados da resposta**

Dados do local:

| Campo     | Tipo    | Exemplo                                                                    |
|-----------|---------|----------------------------------------------------------------------------|
| id        | int     | 1                                                                          |
| nome      | string  | Padaria do Sabor                                                           |
| endereco  | string  | av jardim japao, 98 - Centro - SBC                                         |
| contato   | string  | Whats: 11 99712-3550                                                       |
| descricao | string  | Padaria do bairro                                                          |
| imagem    | string  | http://localhost:8080/imagens/yXNmbLqtqgIaMyVyhQGDCZuIJMwSQ5UQMV6ystLs.png |                  |
| usuario   | Usuario | -                                                                          |

Dados do usuário:

| Campo                 | Tipo   | Exemplo       |
|-----------------------|--------|---------------|
| nome                  | srting | João da Silva |
| email                 | srting | joao@mail.com |

**Exemplo de requisição**

```
POST /api/locais HTTP/1.1
Host: localhost:8080
Content-Type: application/json
Accept: */*

{
  "nome": "Padaria do Sabor",
  "endereco": "av jardim japao, 98 - Centro - SBC",
  "contato": "Whats: 11 99712-3550",
  "descricao": "padaria do bairro",
  "usuario": {
    "nome": "João da Silva",
    "email": "joao@mail.com",
    "password": "senha@123",
    "password_confirmation": "senha@123"
  }
}
```

**Exemplos de respostas**

Dados válidos:

```
HTTP/1.1 201
Content-Type: application/json

{
  "id": 1,
  "nome": "Padaria do Sabor",
  "endereco": "av jardim japao, 98 - Centro - SBC",
  "contato": "Whats: 11 99712-3550",
  "descricao": "padaria do bairro",
  "imagem": null,
  "usuario": {
    "id": 1,
    "nome": "João da Silva",
    "email": "joao@mail.com"
  },
  "links": [
    {
      "type": "GET",
      "rel": "self",
      "uri": "/api/locais"
    },
    {
      "type": "PUT",
      "rel": "atualizar_local",
      "uri": "/api/locais"
    },
    {
      "type": "DELETE",
      "rel": "apagar_local",
      "uri": "/api/locais"
    },
    {
      "type": "POST",
      "rel": "definir_imagem_local",
      "uri": "/api/locais/imagem"
    },
    {
      "type": "GET",
      "rel": "listar_objetos_local",
      "uri": "/api/objetos"
    },
    {
      "type": "POST",
      "rel": "adicionar_objeto_local",
      "uri": "/api/objetos"
    }
  ]
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
  "usuario.email": [
    "O campo usuario.email já está sendo utilizado."
  ]
}
```

### Rota POST /api/locais/imagem

**Dados da requisição**

| Campo        | Tipo | Exemplo |
|--------------|------|---------|
| imagem_local | file | -       |

Regras de validação da imagem do local:

- `imagem_local`: não pode ser nulo
- `imagem_local`: deve ser uma arquivo de imagem

**Dados da resposta**

| Campo    | Tipo   | Exemplo                      |
|----------|--------|------------------------------|
| mensagem | string | Imagem definida com sucesso! |

**Exemplo de requisição**

```
POST /api/locais/imagem HTTP/1.1
Host: localhost:8080
Content-Type: multipart/form-data
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDU4NTksImV4cCI6MTY0MjQ0OTQ1OSwibmJmIjoxNjQyNDQ1ODU5LCJqdGkiOiJJdFV1QzA5Q1VGQ0JoTDdpIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.CjMddVkovYEawKXNwuMroajTKb52R4X3dC5NvH1ClW0
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

## Front-end

## Telas

Para esse caso de uso a tela à ser desenvolvida é a tela de cadastro de local e usuário.

### Tela de Cadastro

Essa tela deve conter dois formulários, um para receber os dados do local e outro para receber os dados do usuário, além disso ela também deve conter uma botão com o texto "Cadastrar-se" que ao ser clicado pelo usuário deve então validar todos os dados informados e caso estejam válidos os enviará para a api que irá então realizar o cadastro dos dados informados.

![Tela de cadastro da local](../telas/tela-novo-usuario-na-plataforma.png)

## RAP07 - Realizar login

Abaixo você encontrará todas as informações do quê e como deve ser desenvolvido no back-end e no front-end para o caso de uso RAP07.

## Back-end

## Rotas

| Rota              | Verbo HTTP | Descrição                                                                       |
|-------------------|------------|---------------------------------------------------------------------------------|
| /api/auth/login   | POST       | Rota responsável por gerar tokens de acesso a partir das credenciais do usuário |
| /api/auth/refresh | POST       | Rota responsável por gerar os tokens de acesso a partir do refresh token        |
| /api/auth/logout  | POST       | Rota responsável por invalidar os tokens de acesso de um usuário                |
| /api/locais       | GET        | Rota responsável por exibir os dados do usuário logado                          |

### Rota POST /api/auth/login

**Dados da requisição**

| Campo    | Tipo    | Exemplo       |
|----------|---------|---------------|
| email    | string  | joao@mail.com |
| password | string  | senha@123     |

Regras de validação:

- `email`: não pode ser nulo
- `email`: não pode ser vazio
- `email`: não pode ser menor que 3 caracteres
- `email`: não pode ser maior que 255 caracteres
- `email`: deve haver algum usuário cadastrado com esse `email`
- `password`: não pode ser nulo
- `password`: não pode ser vazio
- `password`: deve ser igual a senha cadastrada para o usuário encontrado

**Dados da resposta**

| Campo   | Tipo   | Exemplo                                                                                                                                                                                                                                                                                                                                                               |
|---------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| access  | string | eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDE4MzA4NTUsImV4cCI6MTY0MTgzNDQ1NSwibmJmIjoxNjQxODMwODU1LCJqdGkiOiJqSmhkOURDTmFobXFOR0hIIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.2UnX43gzSDWOfhO5XlUFPu0DZptufMUz7AWsHQb8s7o |
| refresh | string | eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDE4MzA4NTUsImV4cCI6MTY0MTgzNDQ1NSwibmJmIjoxNjQxODMwODU1LCJqdGkiOiJqSmhkOURDTmFobXFOR0hIIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.2UnX43gzSDWOfhO5XlUFPu0DZptufMUz7AWsHQb8s7o |

**Exemplo de requisição**

```
POST /api/auth/login HTTP/1.1
Host: localhost:8080
Content-Type: application/json
Accept: */*

{
  "email": "joao@mail.com",
  "password": "senha@123"
}
```

**Exemplos de respostas**

Dados válidos:

```
HTTP/1.1 200
Content-Type: application/json

{
  "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDE4MzA4NTUsImV4cCI6MTY0MTgzNDQ1NSwibmJmIjoxNjQxODMwODU1LCJqdGkiOiJqSmhkOURDTmFobXFOR0hIIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.2UnX43gzSDWOfhO5XlUFPu0DZptufMUz7AWsHQb8s7o",
  "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDE4MzA4NTUsImV4cCI6MTY0MTgzNDQ1NSwibmJmIjoxNjQxODMwODU1LCJqdGkiOiJqSmhkOURDTmFobXFOR0hIIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.2UnX43gzSDWOfhO5XlUFPu0DZptufMUz7AWsHQb8s7o"
}
```

Dados inválidos:

```
HTTP/1.1 401
Content-Type: application/json

{
  "mensagem": "Unauthorized"
}
```

### Rota POST /api/auth/refresh

**Dados da requisição**

| Campo   | Tipo   | Exemplo                                                                                                                                                                                  |
|---------|------- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| refresh | string | eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJqb2FvQG1haWwuY29tIiwiZXhwIjoxNjQyMDQxMTU1LCJpYXQiOjE2NDIwNDEwMzV9.6sa7y4E5xlHzhSUS-0arc9-uCwvBIYvD9YTWYSlLKCjLNk0QXnSfn-cY9P3OAhM0l9Qx0LWB8VG0Gu1kkEhSmQ |

Regras de validação:

- `refresh`: não pode ser nulo
- `refresh`: não pode ser vazio
- `refresh`: deve ser um token válido

**Dados da resposta**

| Campo   | Tipo   | Exemplo                                                                                                                                                                                                                                                                                                                                                               |
|---------|--------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| access  | string | eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDE4MzA4NTUsImV4cCI6MTY0MTgzNDQ1NSwibmJmIjoxNjQxODMwODU1LCJqdGkiOiJqSmhkOURDTmFobXFOR0hIIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.2UnX43gzSDWOfhO5XlUFPu0DZptufMUz7AWsHQb8s7o |
| refresh | string | eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDE4MzA4NTUsImV4cCI6MTY0MTgzNDQ1NSwibmJmIjoxNjQxODMwODU1LCJqdGkiOiJqSmhkOURDTmFobXFOR0hIIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.2UnX43gzSDWOfhO5XlUFPu0DZptufMUz7AWsHQb8s7o |

**Exemplo de requisição**

```
POST /api/auth/refresh HTTP/1.1
Host: localhost:8080
Content-Type: application/json
Accept: */*

{
  "refresh": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJqb2FvQG1haWwuY29tIiwiZXhwIjoxNjQyMDQxMTU1LCJpYXQiOjE2NDIwNDEwMzV9.6sa7y4E5xlHzhSUS-0arc9-uCwvBIYvD9YTWYSlLKCjLNk0QXnSfn-cY9P3OAhM0l9Qx0LWB8VG0Gu1kkEhSmQ"
}
```

**Exemplos de respostas**

Dados válidos:

```
HTTP/1.1 200
Content-Type: application/json

{
  "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDE4MzA4NTUsImV4cCI6MTY0MTgzNDQ1NSwibmJmIjoxNjQxODMwODU1LCJqdGkiOiJqSmhkOURDTmFobXFOR0hIIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.2UnX43gzSDWOfhO5XlUFPu0DZptufMUz7AWsHQb8s7o",
  "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDE4MzA4NTUsImV4cCI6MTY0MTgzNDQ1NSwibmJmIjoxNjQxODMwODU1LCJqdGkiOiJqSmhkOURDTmFobXFOR0hIIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.2UnX43gzSDWOfhO5XlUFPu0DZptufMUz7AWsHQb8s7o"
}
```

Dados inválidos:

```
HTTP/1.1 401
Content-Type: application/json

{
  "mensagem": "Unauthorized"
}
```

### Rota POST /api/auth/logout

**Dados da requisição**

Não se aplica

**Dados da resposta**

| Campo    | Tipo   | Exemplo                      |
|----------|--------|------------------------------|
| mensagem | string | Logout realizado com sucesso |

**Exemplo de requisição**

```
POST /api/auth/logout HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDY3MjAsImV4cCI6MTY0MjQ1MDMyMCwibmJmIjoxNjQyNDQ2NzIwLCJqdGkiOiJhdzNmak9GNjFTT2JKNTRHIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.NweLZ_H8k2ZaCbPXh0gPvaimaGwnWszB5ypEUx-sKII
Accept: */*
```

**Exemplos de respostas**

Dados válidos:

```
HTTP/1.1 200
Content-Type: application/json

{
  "message": "Logout realizado com sucesso"
}
```

Token inválido:

```
HTTP/1.1 401
Content-Type: application/json

{
  "message": "Unauthenticated."
}
```

## Front-end

## Telas

Para esse caso de uso a tela que deve ser desenvolvida é a tela de login.

### Tela de login

Essa tela deve conter um formulário que irá receber os email e a senha do usuário que está tentando se logar, além disso também terá um botão com o texto "Entrar" que ao ser clicado pelo usuário irá realizar as devidas válidações dos dados e caso estejam validos irá enviar essas infromações ao back-end para que o mesmo possa então realizar o processo de autenticação.

![Tela de login na aplicação](../telas/tela-realizar-login.png)
