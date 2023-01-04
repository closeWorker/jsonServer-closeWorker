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
<h2 align ='center'> Possíveis erros </h2>

Email já cadastrado:

`POST /register - `
` FORMATO DA RESPOSTA - STATUS 400`

```json
"Email already exists"
```
<h2 align ='center'> Observaçõess </h2>

Por limitação de conhecimento a respeito das configurações do json server, não será retornado erros, caso a requisição seja enviada faltando algum item obrigatório, assim recomendamos atenção ao criar o objeto json , que será enviado na requisição de registro.
