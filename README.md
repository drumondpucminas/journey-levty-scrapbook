# Etapa 2: API para o Departamento de Polícia

## 🧩 Contexto

A Polícia está modernizando seus sistemas e criou um novo serviço digital para rastrear **casos, e agentes da corporação**. 

Você foi convocado para desenvolver a **primeira versão da API REST**, que permitirá aos investigadores cadastrar, consultar e atualizar informações — tudo operando em um servidor **Node.js com Express**.

---

## 🎯 Objetivo

Construir uma **API RESTful** que permita o gerenciamento de **agentes,e casos policiais fictícios**, com validações, tratamento de erros e dados armazenados **em memória** (utilizando arrays).

--- 

## Como Iniciar o Servidor

Siga os passos abaixo para configurar e rodar o projeto em sua máquina local.

**1. Crie o projeto seguindo a estrutura**

Clone o repositório e execute o seguinte comando: 

```npm init -y```

Depois, crie os repositórios e arquivos e diretórios seguindo a estrutura de exemplo (está descrita abaixo).

**2. Instale as Dependências**

Navegue até o diretório raiz do projeto pelo terminal e instale o Express.js:

```bash
npm install express
```
Se você estiver recebendo os dados do formulário via POST, precisará de um middleware para interpretar o corpo da requisição. O Express já inclui o express.urlencoded.

**Observação:** não devem ser utilizadas outras dependências além do express, como template engines.

**3. Crie o servidor**

Insira este código no arquivo server.js

```javascript
const express = require('express')
const app = express();
const PORT = 3000;

app.listen(PORT, () => {
    console.log(`Servidor da DevBurger rodando em localhost:${PORT}`);
});
```

**4. Inicie o Servidor**

Execute o seguinte comando no terminal:

```bash
npm start
```

O servidor será iniciado, e você deverá ver uma mensagem no console, por exemplo:

Servidor da DevBurger rodando em http://localhost:3000

Agora, você pode abrir seu navegador e acessar http://localhost:3000. O texto "Hello World!" deverá ser exibido no seu navegador.
## Orientações Gerais para a atividade
### Controladores
Nessa etapa vamos modularizar nosso código e utilizar os controladores para servir as rotas. Os dois arquivos de controladores devem receber os nomes indicados abaixo e devem residir na pasta `/controllers` 
### Rotas
As rotas nessa etapa devem ser definidas no arquivo `routes.js`, porém dessa vez utilizaremos o Router do express, segue um exemplo de como utilizá-lo um exemplo presente na documentação oficial do express abaixo:
```javascript
const express = require('express')
const router = express.Router();
const PORT = 3000;

// define a rota base
router.get('/', (req, res) => {
  res.send('Birds home page')
})
// define a rota /about
router.get('/about', (req, res) => {
  res.send('About birds')
})

module.exports = router
```
Agora adicionaremos o `router` como middleware no arquivo principal da aplicação:

```javascript
//server.js 

const express = require('express');
const app = express();

app.use(router);

app.listen(PORT, () => {
    console.log(`Servidor da DevBurger rodando em http://localhost:${PORT} em modo de desenvolvimento`);
}); 
 ```

 
---
# 📁  Estrutura dos Diretórios (pastas) 
```
📦 SEU-REPOSITÓRIO
├── 📁 .github
│   └── 📁 workflows
│       └── classroom.yml         
│
├── 📁 controllers
│   ├── agentesController.js      
│   └── casosController.js        

├── server.js
├── routes.js                     
├── README.md                     
```
- O Router do express e as rotas da API devem estar no `routes.js`.
- Os controladores devem estar na pasta `/controllers`
- Não delete a pasta `.github, é por lá que o **Autograder** reside.
---
# 📙 Recurso de casos policiais: `/casos`

Gerencia os **registros de crimes nos arquivos do departamento de polícia**.

### Métodos HTTP que deverão ser implementados:
- `GET /casos` → Lista todos os casos registrados. 
- `GET /casos/:id` → Retorna os detalhes de um caso específico.
- `POST /casos` → Cria um novo caso com os seguintes campos:
- `PUT /casos/:id` → Atualiza os dados de um caso por completo.
- `PATCH /casos/:id` → Atualiza os dados de um caso parcialmente.
- `DELETE /casos/:id` → Remove um caso do sistema.
## Bônus
- `GET /casos?agente_id=uuid` → Lista todos os casos atribuídos à um agente específico.
- `GET /casos/:caso_id?agente_id=uuid` → Retorna os dados completos do agente responsável por um caso específico.
- `GET /casos?status=aberto` → Lista todos os casos em aberto.


#### Estrutura de um caso:
  - `id`: string (UUID) **obrigatório**.
  - `titulo`: string **obrigatório**.
  - `descricao`: string **obrigatório**.
  - `status`: deve ser `"aberto"` ou `"solucionado"` **obrigatório**.
  - `agente_id`: string (UUID), id do agente responsável

### Regras e Validações:

- `titulo` e `descricao` são obrigatórios.
- `status` deve ser `"aberto"` ou `"solucionado"`.
- IDs inexistentes devem retornar status **404**.
- Dados mal formatados devem retornar status **400**.
- Status HTTP esperados: **201**, **200**, **204**, **400**, **404**.

---

# 📙 Recurso de agentes policiais: `/agentes`

Gerencia os **agentes da polícia**.

### Métodos HTTP que deverão ser implementados::

- `GET /agentes` → Lista todos os agentes.
- `GET /agentes/:id` → Retorna um agente específico.
- `POST /agentes` → Cadastra um novo agente com:
- `PUT /agentes/:id` → Atualiza os dados do agente por completo.
- `PATCH /agentes/:id` → Atualiza os dados do agente parcialmente.
- `DELETE /agentes/:id` → Remove o agente.

## Bônus

- `GET /agentes/inspetores` → Lista todos os agentes de cargo "inspetor".
- `GET /agentes/delegados` → Lista todos os agentes de cargo "delegado".
- `GET /agentes/senioridade` → Lista os agentes em ordem decrescente de data incorporação, do mais velho para o mais novo


#### Estrutura de um agente:
  - `id`: string (UUID) **obrigatório**.
  - `nome`: string **obrigatório**.
  - `dataDeIncorporacao`: string , no formato `YYYY-MM-DD`**obrigatória**.
  - `cargo`: ("inspetor", "delegado", etc.) **obrigatório**.

### Regras e Validações:

- IDs inválidos devem retornar status **404**.
- Dados mal formatados devem retornar status **400**.
- IDs inexistentes devem retornar status **404**.
- Status HTTP esperados: **201**, **200**, **204**, **400**, **404**.


---
# 📝 Orientações gerais para respostas
### Requisições GET
- As requisições do tipo `GET` devem retornar o status code **200 OK✅** e o objeto ou array de objetos do recurso.
### Requisições POST, PUT e PATCH
- As requisições do tipo `PUT` e `PATCH` devem retornar o status code **200 OK✅** e o objeto atualizado!
- As requisições do tipo `POST` devem retornar o status code **201 CREATED✅** e o objeto criado!
### Requisições DELETE
- As requisições do tipo `DELETE`devem retornar o status code **204 NO CONTENT✅** e não devem possuir corpo de resposta.









