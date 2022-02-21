# Quarta Entrega

## Descrição

Durante essa entrega você terá que desenvolver as rotas e telas referentes as funcionalidades de informe de entrega do objeto ao dono, alteração dos dodos do local/usuário e exclusão da conta.

## Requisitos Funcionais

Os requisitos funcionais que estão relacionados com essa entrega são:

- **RAP06 - Informar dono do objeto**: O administrador do departamento de achados e perdidos deverá informar a entrega de um objeto ao dono. O sistema deverá solicitar o nome e CPF do dono. Após definido como entregue o objeto não poderá mais ser exibido na plataforma.

- **RAP08 - Alterar dados cadastrais**: O sistema deverá permitir ao administrador do departamento de achados e perdidos alterar seus dados de acesso, além dos dados do local que ele é responsável.

- **RAP09 - Apagar local**: O administrador do departamento de achados e perdidos poderá excluir o local da plataforma. O sistema deve excluir também os dados e acesso e os objetos do local.

## RAP06 - Informar dono do objeto

Abaixo você encontrará todas as informações do quê e como deve ser desenvolvido no back-end e no front-end para o caso de uso RAP06.

## Back-end

### Rotas

| Rota                          | Verbo HTTP | Descrição                                               |
|-------------------------------|------------|-------------------------------------------------------- |
| /api/objetos/{objetoId}/donos | POST       | Rota responsável por definir os dados do dono do objeto |

### Rota POST /api/objetos/{objetoId}/donos

**Dados no cabeçalho da requisição**

| Chave         | Tipo   | Exemplo                                                                                                                                                                                                                                                                                                                                                                      |
|---------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authorization | string | Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDU4NTksImV4cCI6MTY0MjQ0OTQ1OSwibmJmIjoxNjQyNDQ1ODU5LCJqdGkiOiJJdFV1QzA5Q1VGQ0JoTDdpIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.CjMddVkovYEawKXNwuMroajTKb52R4X3dC5NvH1ClW0 |

**Dados no corpo da requisição**

| Campo     | Tipo    | Exemplo       |
|-----------|---------|---------------|
| dono_nome | string  | João da Silva |
| dono_cpf  | string  | 39432797589   |

Regras de validação do local:

- `dono_nome`: não pode ser nulo
- `dono_nome`: não pode ser vazio
- `dono_nome`: não pode ser menor que 3 caracteres
- `dono_nome`: não pode ser maior que 255 caracteres
- `dono_cpf`: não pode ser nulo
- `dono_cpf`: não pode ser vazio
- `dono_cpf`: não pode ser menor que 11 caracteres
- `dono_cpf`: não pode ser maior que 11 caracteres
- `dono_cpf`: deve ser um cpf válido

**Dados da resposta**

| Campo    | Tipo   | Exemplo                             |
|----------|--------|-------------------------------------|
| mensagem | string | Dono do objeto definido com sucesso |

**Exemplo de requisição**

```
PATCH /api/objetos/64/donos HTTP/1.1
Host: localhost:8080
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0Njk5OTAsImV4cCI6MTY0MjQ3MzU5MCwibmJmIjoxNjQyNDY5OTkwLCJqdGkiOiI3VVhCNFFkV2dHVGxrRHdDIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.58A_CMkeTN5lGGeUhA-cJtQeoJPmDFUu8bgDhfhQN5E
Accept: */*

{
	"dono_nome": "João da Silva",
	"dono_cpf": "39432797589"
}
```

**Exemplos de respostas**

Dados válidos:

```
HTTP/1.1 200
Content-Type: application/json

{
	"message": "Dono do objeto definido com sucesso"
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
	"dono_nome": [
		"O campo dono nome é obrigatório."
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

Para esse caso de uso a tela à ser desenvolvida é a para informar o dono do objeto.

### Tela de Cadastro

Essa tela deve conter um formulário para que o usuário possa informar os dados do dono do objeto.

![Tela de informar dono do objeto](../telas/tela-informar-dono-objeto.png)

## RAP08 - Alterar dados cadastrais

Abaixo você encontrará todas as informações do quê e como deve ser desenvolvido no back-end e no front-end para o caso de uso RAP08.

## Back-end

### Rotas

| Rota        | Verbo HTTP | Descrição                                                   |
|-------------|------------|-------------------------------------------------------------|
| /api/locais | PUT        | Rota responsável por alterar os dados do local e do usuário |

### Rota PUT /api/locais

**Dados no cabeçalho da requisição**

| Chave         | Tipo   | Exemplo                                                                                                                                                                                                                                                                                                                                                                      |
|---------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Authorization | string | Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9hY2hhZG9zLWUtcGVyZGlkb3MtcGhwLmhlcm9rdWFwcC5jb21cL2FwaVwvYXV0aFwvbG9naW4iLCJpYXQiOjE2NDI0NDU4NTksImV4cCI6MTY0MjQ0OTQ1OSwibmJmIjoxNjQyNDQ1ODU5LCJqdGkiOiJJdFV1QzA5Q1VGQ0JoTDdpIiwic3ViIjo2MSwicHJ2IjoiMjNiZDVjODk0OWY2MDBhZGIzOWU3MDFjNDAwODcyZGI3YTU5NzZmNyJ9.CjMddVkovYEawKXNwuMroajTKb52R4X3dC5NvH1ClW0 |

**Dados no corpo da requisição**

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
PUT /api/locais HTTP/1.1
Host: localhost:8080
Content-Type: application/json
Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJlbHRvbi5mb25zZWNhQHRyZWluYXdlYi5jb20uYnIiLCJleHAiOjE2NDIyMDY5ODIsImlhdCI6MTY0MjIwNjkyMn0.s6pp1Zw8Bhn3-i28BBf75sDpMSWFmo_XsHWuNRTFGgDwYOxg_F7FbIKhCfpRG5ncbiA5kaixZL9xBfVsfHWHdA
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
HTTP/1.1 200
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

Para esse caso de uso a tela à ser desenvolvida é a tela para atualizar os dados do local e do usuário.

### Tela de Cadastro

Essa tela deve conter dois formulários, um para receber os dados do local e outro para receber os dados do usuário, esses formulários deve ser exibidos já preenchidos com os dados do local e do usuáro, além disso ela também deve conter uma botão com o texto "Atualizar" que ao ser clicado pelo usuário deve então validar todos os dados informados e caso estejam válidos os enviará para a api que irá então realizar a atualização do cadastro. Por fim também deve haver um botão com o texto "Excluir local".

![Tela de informar dono do objeto](../telas/tela-alterar-dados-local-usuario.png)

## RAP09 - Apagar local

Abaixo você encontrará todas as informações do quê e como deve ser desenvolvido no back-end e no front-end para o caso de uso RAP09.

## Back-end

### Rotas

| Rota        | Verbo HTTP | Descrição                                        |
|-------------|------------|--------------------------------------------------|
| /api/locais | DELETE     | Rota responsável por excluir o usuário e o local |

### Rota DELETE /api/locais

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
DELETE /api/locais HTTP/1.1
Host: localhost:8080
Authorization: Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJlbHRvbi5mb25zZWNhQHRyZWluYXdlYi5jb20uYnIiLCJleHAiOjE2NDIyMDY5ODIsImlhdCI6MTY0MjIwNjkyMn0.s6pp1Zw8Bhn3-i28BBf75sDpMSWFmo_XsHWuNRTFGgDwYOxg_F7FbIKhCfpRG5ncbiA5kaixZL9xBfVsfHWHdA
Accept: */*
```

**Exemplos de respostas**

Token válido:

```
HTTP/1.1 204
Content-Type: application/json
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

Para esse caso de uso não será necessário o desenvolvimento de nenhuma tela, pois a funcionalidade será executada a partir do botão excluir local localizado na tela de alteração dos dados do local e do usuário
