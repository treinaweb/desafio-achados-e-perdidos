# Casos de Uso

## DOP01 - Procurar um Objeto

O dono de um objeto perdido poderá realizar a busca. O sistema deve permitir que ele busque o local por onde passou no dia que perdeu o objeto. Se o local tiver cadastro, deve ser exibida a lista com os objetos disponíveis para retirada. Por fim, se o objeto tiver disponível, o sistema deve apresentar os contatos do departamento de achados e perdidos do local.

### Precondição

Nenhuma

### Ator

Dono Objeto

### Fluxo de eventos

![Diagram do fluxo de eventos do caso de uso DOP01](../out/casos-de-uso/dono-objeto/DOP01/DOP01.png)

## RAP01 - Cadastrar local

O administrador do departamento de achados e perdidos poderá realizar o cadastro do local na plataforma. O sistema deve permitir que ele entre com os dados do local e as informações de acesso à plataforma.

### Precondição

Nenhuma

### Ator

Administrador departamento de achados e perdidos

### Fluxo de eventos

![Diagram do fluxo de eventos do caso de uso RAP01](../out/casos-de-uso/administrador/RAP01/RAP01.png)

## RAP02 - Listar objetos do local

O administrador do departamento de achados e perdidos poderá realizar a listagem dos objetos cadastrados para o local.

### Precondição

O usuário deve estar logado no sistema como um dos atores do caso de uso.

### Ator

Administrador departamento de achados e perdidos

### Fluxo de eventos

![Diagram do fluxo de eventos do caso de uso RAP02](../out/casos-de-uso/administrador/RAP02/RAP02.png)

## RAP03 - Cadastrar objeto para o local

O administrador do departamento de achados e perdidos poderá realizar o cadastro de um objeto para o local.

### Precondição

O usuário deve estar logado no sistema como um dos atores do caso de uso.

### Ator

Administrador departamento de achados e perdidos

### Fluxo de eventos

![Diagram do fluxo de eventos do caso de uso RAP03](../out/casos-de-uso/administrador/RAP03/RAP03.png)

## RAP04 - Editar informações do objeto

O administrador do departamento de achados e perdidos poderá realizar a edição das informações de um objeto previamente cadastrado para o local.

### Precondição

O usuário deve estar logado no sistema como um dos atores do caso de uso.

### Ator

Administrador departamento de achados e perdidos

### Fluxo de eventos

![Diagram do fluxo de eventos do caso de uso RAP04](../out/casos-de-uso/administrador/RAP04/RAP04.png)

## RAP05 - Informar dono do objeto

O administrador do departamento de achados e perdidos deverá informar a entrega de um objeto ao dono. O sistema deverá solicitar o nome e CPF do dono. Após definido como entregue, o objeto não poderá mais ser exibido na plataforma.

### Precondição

O usuário deve estar logado no sistema como um dos atores do caso de uso.

### Ator

Administrador departamento de achados e perdidos

### Fluxo de eventos

![Diagram do fluxo de eventos do caso de uso RAP05](../out/casos-de-uso/administrador/RAP05/RAP05.png)

## RAP06 - Realizar login

O administrador do departamento de achados e perdidos poderá realizar login na plataforma. Após o login ele deve ser direcionado para a lista de objetos.

### Precondição

O usuário deve estar cadastrado no sistema como um dos atores do caso de uso.

### Ator

Administrador departamento de achados e perdidos

### Fluxo de eventos

![Diagram do fluxo de eventos do caso de uso RAP06](../out/casos-de-uso/administrador/RAP06/RAP06.png)

## RAP07 - Alterar dados cadastrais

O sistema deverá permitir ao administrador do departamento de achados e perdidos alterar suas informações de acesso, além dos dados do local que ele é responsável.

### Precondição

O usuário deve estar logado no sistema como um dos atores do caso de uso.

### Ator

Administrador departamento de achados e perdidos

### Fluxo de eventos

![Diagram do fluxo de eventos do caso de uso RAP07](../out/casos-de-uso/administrador/RAP07/RAP07.png)

## RAP08 - Apagar local

O administrador do departamento de achados e perdidos poderá excluir o local da plataforma. O sistema deve excluir também os dados e acesso e os objetos do local.

### Precondição

O usuário deve estar logado no sistema como um dos atores do caso de uso.

### Ator

Administrador departamento de achados e perdidos

### Fluxo de eventos

![Diagram do fluxo de eventos do caso de uso RAP08](../out/casos-de-uso/administrador/RAP08/RAP08.png)
