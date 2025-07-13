# Etapa 2: API para o Departamento de Polícia

## 🧩 Contexto

A Polícia está modernizando seus sistemas e criou um novo serviço digital para rastrear **casos, denúncias e agentes da corporação**. 

Você foi convocado para desenvolver a **primeira versão da API REST**, que permitirá aos investigadores cadastrar, consultar e atualizar informações — tudo operando em um servidor **Node.js com Express**.

---

## 🎯 Objetivo

Construir uma **API RESTful** que permita o gerenciamento de **agentes, denúncias e casos policiais fictícios**, com validações, tratamento de erros e dados armazenados **em memória** (utilizando arrays).

---

#  Recurso de casos policiais: `/casos`

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

#  Recurso de agentes policiais: `/agentes`

Gerencia os **agentes da polícia**.

### Métodos HTTP que deverão ser implementados::

- `GET /agentes` → Lista todos os agentes.
- `GET /agentes/:id` → Retorna um agente específico.
- `POST /agentes` → Cadastra um novo agente com:
- `PUT /agentes/:id` → Atualiza os dados do agente por completo.
- `PATCH /agentes/:id` → Atualiza os dados do agente parcialmente.
- `DELETE /agentes/:id` → Remove o agente.

## Bônus

- `GET /agentes/inspetores` → Lista todos os agentes de cargo "Inspetor".
- `GET /agentes/delegados` → Lista todos os agentes de cargo "Delegado".


#### Estrutura de um agente:
  - `id`: string (UUID) **obrigatório**.
  - `nome`: string **obrigatório**.
  - `anoDeEntrada`: string , no formato `YYYY-MM-DD`**obrigatória**.
  - `cargo`: ("Inspetor", "Delegado", etc.) **obrigatório**.

### Regras e Validações:

- IDs inválidos devem retornar status **404**.
- Dados mal formatados devem retornar status **400**.
- IDs inexistentes devem retornar status **404**.
- Status HTTP esperados: **201**, **200**, **204**, **400**, **404**.


---





