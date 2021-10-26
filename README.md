<h1 align="center">
  Atividade - JSON-Server do início ao Deploy
</h1>

<p align = "center">
Esta é uma Fake-API hospedada no Heroku onde é possível realizar requisições seguindo os parâmetros abaixo.
</p>

<p align="center">
  <a href="#endpoints">Endpoints</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</p>


## **Endpoints**

A API tem um total de 3 endpoints, sendo em volta principalmente do usuário - podendo cadastrar seu perfil, pets e necessidades para os cuidados de pets. <br/>
O JSON para utilizar no Insomnia é este aqui -> https://git.heroku.com/atividade-json.git

Para importar o JSON no Insomnia é só clicar na palavra "Insomnia" no canto superior esquerdo. Nesse dropdown é só clicar em "Import / Export > Import Data > From Url" e colocar o link acima :v:

O url base da API é https://atividade-json.herokuapp.com/

## Rotas que não precisam de autenticação

<h2 align ='center'> Criação de usuário </h2>

`POST /register -  FORMATO DA REQUISIÇÃO`
```json
{
"email": "maria1@gmail.com",
"password": "123456",
"name": "Maria",
"age": 19,
}
```

Caso dê tudo certo, a resposta será assim:

`POST /register -  FORMATO DA RESPOSTA - STATUS 201`
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hcmlhMUBnbWFpbC5jb20iLCJpYXQiOjE2MzUyNjMyMjAsImV4cCI6MTYzNTI2NjgyMCwic3ViIjoiNCJ9.krTbGZCo6unxYsAUcwfMoxTU2GXj323DRhD_YEePMSk",
  "user": {
    "email": "maria1@gmail.com",
    "name": "Maria",
    "age": 19,
    "id": 4
  }
}
```

<h2 align ='center'> Possíveis erros </h2>
```

Email já cadastrado:

`POST /register - `
``  FORMATO DA RESPOSTA - STATUS 400``
```json

 "Email already exists"

```

<h2 align = "center"> Login </h2>

`POST /login - FORMATO DA REQUISIÇÃO`
```json
{
"email": "maria@gmail.com",
"password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /register -  FORMATO DA RESPOSTA - STATUS 201`
```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hcmlhQGdtYWlsLmNvbSIsImlhdCI6MTYzNTI2MzQ2MCwiZXhwIjoxNjM1MjY3MDYwLCJzdWIiOiIyIn0.L90h-Byt7fGgAhtw1uKX9QntsIwSjOs3fRf20Jcv-kc",
  "user": {
    "email": "maria@gmail.com",
    "name": "Maria",
    "age": 19,
    "id": 2
  }
}
```

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.

<h2 align ='center'> Criação de animais. </h2>

`POST /animals -  FORMATO DA RESPOSTA - STATUS 200`
```json
[
  {
    "type": "maria@gmail.com",
    "name":"Laila",
    "userId": 2
  }
]

```

<h2 align ='center'> Listando animais. </h2>

`GET /animals -  FORMATO DA RESPOSTA - STATUS 200`
```json
[
  {
    "type": "Gato",
    "name": "bigodes",
    "userId": 1,
    "id": 1
  },
  {
    "type": "Cachorro",
    "name": "Laila",
    "userId": 2,
    "id": 2
  }
]

```

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

Após o usuário estar logado, ele deve conseguir ler suas informações.

<h2 align ='center'> Listando informações do usuário. </h2>

Nessa aplicação o usuário precisa fazer login ou se cadastrar para ver suas informações já cadastradas na plataforma, na API podemos acessar dessa forma:
Aqui conseguimos ver o email, sua senha criptografada, nome, idade e id de usuário.

`GET /users/:id -  FORMATO DA RESPOSTA - STATUS 200`
```json
[
  {
    "email": "maria@gmail.com",
    "password":"$2a$10$FrCgIhKxdWF8OLmtgHfVlvm6wkyykUwL2sKy8Oyf2KjwRg1JL2",
    "name": "Maria",
    "age": 19,
    "id": 2
  }
]

```

<h2 align ='center'> Ver as necessidades. </h2>

`GET /needs -  FORMATO DA RESPOSTA - STATUS 200`
```json
[
  {
    "level": "Ração",
    "id": 1
  },
  {
    "level": "Água",
    "id": 2
  }
]

```

<h2 align ='center'> Criar necessidade. </h2>

`POST /needs - FORMATO DA REQUISIÇÃO`
```json
{
  "need": "Dar banho"
}
```

---
Feito com ♥ by maria-baia :wave:
