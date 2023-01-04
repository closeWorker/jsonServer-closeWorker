<h1 align="center">
  Close Worker - Json-Server
</h1>

<p align = "center">
Este é o json server da aplicação <b>Close Worker</b> -  Uma página de busca de prestadores de serviços autônomos próximos ao usuário, na cidade do Rio de Janeiro – RJ.
</p>

<p align="center">
  <a href="#endpoints">Endpoints</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</p>

## **Endpoints**

A API tem um total de 4 endpoints,  podendo cadastrar seu usuário, realizar login e cadastrar serviços na plataforma. <br/>

<a href="https://insomnia.rest/run/?label=closeWorker-JsonServerAPI&uri=https%3A%2F%2Fraw.githubusercontent.com%2FcloseWorker%2FjsonServer-closeWorker%2Fmain%2FconfigInsomia.json" target="_blank"><img src="https://insomnia.rest/images/run.svg" alt="Run in Insomnia"></a>

<blockquote> Para importar o JSON no Insomnia é só clicar no botão "Run in Insomnia". Depois é só seguir os passos que ele irá importar todos os endpoints em seu insomnia.
</blockquote>
<br>

No momento este json server funciona apenas localmente, assim sua url base é: http://localhost:3001

<h2 align ='center'> Criação de usuário </h2>

`POST /register - FORMATO DA REQUISIÇÃO`

```json
{
	"name": "teste3",
	"email": "teste3@gmail.com",
	"password": "123456ab",
	"contact": "(xx) xxxxx-xxxx",
	"avatar": "teste3.png"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /register - FORMATO DA RESPOSTA - STATUS 201`

```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlM0BnbWFpbC5jb20iLCJpYXQiOjE2NzI4NTA1ODQsImV4cCI6MTY3Mjg1NDE4NCwic3ViIjoiNCJ9.fu3HRIq9kgDj4JHr0N4931dXWTpkirImHUGo4LNrESM",
	"user": {
		"email": "teste3@gmail.com",
		"name": "teste3",
		"contact": "(xx) xxxxx-xxxx",
		"avatar": "teste3.png",
		"id": 4
	}
}
```
<h3 align ='center'> Possíveis erros </h3>

Email já cadastrado:

`POST /register - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
"Email already exists"
```
<h3 align ='center'> Observações </h3>

Por limitação de conhecimento a respeito das configurações do json server, não será retornado erros, caso a requisição seja enviada faltando algum item obrigatório, assim recomendamos atenção ao criar o objeto json , que será enviado na requisição de registro.

<h2 align = "center"> Login </h2>

`POST /login - FORMATO DA REQUISIÇÃO`

```json
{
	"email": "teste3@gmail.com",
	"password": "123456ab"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlM0BnbWFpbC5jb20iLCJpYXQiOjE2NzI4NTM5NjEsImV4cCI6MTY3Mjg1NzU2MSwic3ViIjoiNCJ9.1tbCR_Vde9kMUVieatLxVKCqcwM4rEsOJlc3QkZ9AsM",
	"user": {
		"email": "teste3@gmail.com",
		"name": "teste3",
		"contact": "(xx) xxxxx-xxxx",
		"avatar": "teste3.png",
		"id": 4
	}
}
```

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token no localStorage para fazer a gestão do usuário no seu frontend.

<h3 align ='center'> Possíveis erros </h3>

Email incorreto:

`POST /login - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
"Cannot find user"
```
Senha incorreta:

`POST /login - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
"Incorrect password"
```

<h2 align = "center"> Buscar todos os serviços cadastrados na plataforma </h2>


Não é preciso enviar body, ou token na requisição

`GET /services - FORMATO DA REQUISIÇÃO`


Caso dê tudo certo, a resposta será assim:

`GET /services - FORMATO DA RESPOSTA - STATUS 200`

```json
[
	{
		"userId": 3,
		"service_provider": "teste2",
		"service_provider_avatar": "teste2.png",
		"kink_of_service": "Pedreiro",
		"phone_number": "(xx) xxxxx-xxxx",
		"link_instagram": "https://www.instagram.com/teste2",
		"id": 1
	},
	{
		"userId": 2,
		"service_provider": "teste1",
		"service_provider_avatar": "teste1.png",
		"kink_of_service": "Doceira",
		"phone_number": "(xx) xxxxx-xxxx",
		"link_instagram": "https://www.instagram.com/teste1",
		"id": 4
	}
]
```

<h2 align = "center"> Filtrar os serviços cadastrados na plataforma, pelo tipo</h2>


Não é preciso enviar body, ou token na requisição

`GET /services?kink_of_service=${tipo_do_serviço} - FORMATO DA REQUISIÇÃO`


Caso dê tudo certo, a resposta será assim:

`GET /services?kink_of_service=${tipo_do_serviço} - FORMATO DA RESPOSTA - STATUS 200`

```json
[
	{
		"userId": 3,
		"service_provider": "teste2",
		"service_provider_avatar": "teste2.png",
		"kink_of_service": "Pedreiro",
		"phone_number": "(xx) xxxxx-xxxx",
		"link_instagram": "https://www.instagram.com/teste2",
		"id": 1
	},
	{
		"userId": 2,
		"service_provider": "teste1",
		"service_provider_avatar": "teste1.png",
		"kink_of_service": "Doceira",
		"phone_number": "(xx) xxxxx-xxxx",
		"link_instagram": "https://www.instagram.com/teste1",
		"id": 4
	}
]
```

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Validação de token </h2>

`GET /tokenAuth - FORMATO DA REQUISIÇÃO`
<br>
Só é preciso enviar o token na requisição, o body fica vazio.
<br>
Caso dê tudo certo, a resposta será assim:
<br>
`GET /tokenAuth - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"ok": "Token válido"
}
```
<h3 align ='center'> Erros</h3>

Token não foi enviado:


`GET /tokenAuth - FORMATO DA RESPOSTA - STATUS 401 `

```json
"Missing token"
```

Token não é válido:


`GET /tokenAuth - FORMATO DA RESPOSTA - STATUS 401 `

```json
"invalid signature"
```
<h2 align ='center'> Dados do usuário logado </h2>

`GET /users/${idUsuário} - FORMATO DA REQUISIÇÃO`
<br>
Só é preciso enviar o token na requisição, o body fica vazio.
<br>
Caso dê tudo certo, a resposta será assim:
<br>
`GET /users/${idUsuário} - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"email": "usercoments@gmail.com",
	"password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
	"name": "userComents",
	"contact": "(xx) xxxxx-xxxx",
	"avatar": "userComents.png",
	"id": 1
}
```
<h3 align ='center'> Erros</h3>

Token não foi enviado:


`GET /users/${idUsuário} - FORMATO DA RESPOSTA - STATUS 401 `

```json
"Missing token"
```


Token inválido:


`GET /users/${idUsuário} - FORMATO DA RESPOSTA - STATUS 401 `

```json
"invalid signature"
```


O id utilizado não pertence ao dono do token:


`GET /users/${idUsuário} - FORMATO DA RESPOSTA - STATUS 401 `

```json
"Private resource access: entity must have a reference to the owner id"
```


O id utilizado não existe no banco de dados:


`GET /users/${idUsuário} - FORMATO DA RESPOSTA - STATUS 401 `

```json
"Cannot read properties of undefined (reading 'id')"
```

<h2 align ='center'> Atualizar dados do usuário logado </h2>

`PATCH /users/${idUsuário} - FORMATO DA REQUISIÇÃO`
<br>

```json
{
	"name": "teste111",
	"contact": "(xx) xxxxx-xxxx",
	"avatar": "teste111.png"
}
```

<br>
Caso dê tudo certo, a resposta será assim:
<br>
`GET /users/${idUsuário} - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"email": "teste1@gmail.com",
	"password": "$2a$10$Ir9eXMtbpV4a1GSouLIHkuMX7W9SbNlNpli7z15uURivQOD927w16",
	"name": "teste111",
	"contact": "(xx) xxxxx-xxxx",
	"avatar": "teste111.png",
	"id": 2
}
```

<h2 align ='center'> Serviços cadastrados do usuário logado </h2>

`GET /users/${idUsuário}?_embed=services - FORMATO DA REQUISIÇÃO`
<br>
Só é preciso enviar o token na requisição, o body fica vazio.
<br>
Caso dê tudo certo, a resposta será assim:
<br>
`GET /users/${idUsuário}?_embed=services - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"email": "teste1@gmail.com",
	"password": "$2a$10$h0I5EhMJEH1xubklvQ.L8u1skjLUjOqc0ztjzRZakOmX0yriSThTi",
	"name": "teste1",
	"contact": "(xx) xxxxx-xxxx",
	"avatar": "teste1.png",
	"id": 2,
	"services": [
		{
			"userId": 2,
			"service_provider": "teste1",
			"service_provider_avatar": "teste1.png",
			"kink_of_service": "Doceira",
			"phone_number": "(xx) xxxxx-xxxx",
			"link_instagram": "https://www.instagram.com/teste1",
			"id": 4
		},
		{
			"userId": 2,
			"service_provider": "teste1",
			"service_provider_avatar": "teste1.png",
			"kink_of_service": "Diarista",
			"phone_number": "(xx) xxxxx-xxxx",
			"link_instagram": "https://www.instagram.com/teste1",
			"id": 5
		},
		{
			"userId": 2,
			"service_provider": "teste1",
			"service_provider_avatar": "teste1.png",
			"kink_of_service": "Costureira",
			"phone_number": "(xx) xxxxx-xxxx",
			"link_instagram": "https://www.instagram.com/teste1",
			"id": 6
		}
	]
}
```

<h3 align ='center'> Erros</h3>

Token não foi enviado:


`GET /users/${idUsuário}?_embed=services - FORMATO DA RESPOSTA - STATUS 401 `

```json
"Missing token"
```


Token inválido:


`GET /users/${idUsuário}?_embed=services - FORMATO DA RESPOSTA - STATUS 401 `

```json
"invalid signature"
```


O id utilizado não pertence ao dono do token:


`GET /users/${idUsuário}?_embed=services - FORMATO DA RESPOSTA - STATUS 401 `

```json
"Private resource access: entity must have a reference to the owner id"
```


O id utilizado não existe no banco de dados:


`GET /users/${idUsuário}?_embed=services - FORMATO DA RESPOSTA - STATUS 401 `

```json
"Cannot read properties of undefined (reading 'id')"
```


<h2 align = "center"> Criar um novo serviço </h2>

`POST /services - FORMATO DA REQUISIÇÃO`

```json
{
	"userId": 2,
	"service_provider": "teste1",
	"service_provider_avatar": "teste1.png",
	"kink_of_service": "Servente",
	"phone_number": "(xx) xxxxx-xxxx",
	"link_instagram": "https://www.instagram.com/teste1"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /services - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"userId": 2,
	"service_provider": "teste1",
	"service_provider_avatar": "teste1.png",
	"kink_of_service": "Servente",
	"phone_number": "(xx) xxxxx-xxxx",
	"link_instagram": "https://www.instagram.com/teste1",
	"id": 8
}
```

<h3 align ='center'> Observações </h3>

Por limitação de conhecimento a respeito das configurações do json server, não será retornado erros, caso a requisição seja enviada faltando algum item obrigatório, assim recomendamos atenção ao criar o objeto json , que será enviado na requisição de registro.<br>
O "userId" se refere ao id do usuário logado dono do token enviado.



