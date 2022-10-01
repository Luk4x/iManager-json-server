<table align="right">
  <tr>
    <td>
      <a href="readme-en.md">🇺🇸 English</a>
    </td>
  </tr>
  <tr>
    <td>
      <a href="README.md">🇧🇷 Português</a>
    </td>
  </tr>
</table>
<br>

# 🪙 iManager Project API
> Acesse o projeto [AQUI](https://luk4x-imanager-json-server.herokuapp.com/)
<br>

## Tecnologias utilizadas
- [NodeJS](https://nodejs.org)
- [JSON-Server](https://yarnpkg.com/package/json-server)
- [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

## Sobre
Esse projeto é uma JSON-Server API que realiza o cadastro de projetos e armazena as categorias de projetos de uma plataforma de gestão - a iManager, servindo como base para a sua [Interface](https://github.com/Luk4x/iManager) que desenvolvi essencialmente em [ReactJS](https://pt-br.reactjs.org).

### Rotas
-   `POST /projects`: Essa rota recebe o _nome do projeto_, o _orçamento do projeto_ e a _categoria do projeto_,. essas informações são passadas pelo `body` da requisição, e com base nelas um novo projeto é registrado dentro do array de projetos, no seguinte formato:
    
    ```js
    [
        {
            "name": "Projeto 1",
            "budget": "5000",
            "category": {
                "id": 1,
                "name": "Infra"
            },
            "cost": 0,
            "services": [],
            "id": 1
        }
    ];
    ```

    As informações de `cost` e `services` são inicializadas por padrão no sistema respectivamente como `0` e `[]`, e o `id` é gerado com base na posição do projeto no array, e juntas, essas 3 informações são incorporadas no projeto.<br>

-   `GET /projects`: Essa rota retorna todos os projetos existentes no array de `projects`.

-   `GET /projects/:id`: Com base no `id` enviado, essa rota retorna um projeto específico.

-   `PATCH /projects/:id`: Com base no `id` enviado e nos dados do projeto enviados pelo `body` da requisição, essa rota torna possível atualizar as informações de `name`, `budget` e/ou `category` de um projeto específico.
    Continuando do exemplo acima, ao chamar a rota `PATCH /projects/1` passando `{ order: "X- Salada, 2 batatas grandes, 1 coca-cola", clienteName:"José", price: 44.50 }`, o array fica dessa forma:
    
     ```js
    [
        {
            "name": "Projeto 1",
            "budget": "5000",
            "category": {
                "id": 1,
                "name": "Infra"
            },
            "cost": 0,
            "services": [],
            "id": 1
        }
    ];
    ```

    Através dessa rota, também é possível criar e editar serviços, visto que eles são uma atualiza

-   `DELETE /projects/:id`: Com base no `id` enviado, assim que chamada, essa rota deleta o projeto recebido.

-   `GET /categories`: Essa rota retorna todas as categorias existentes no array de `categories`.


-   `PUT /order/:id`: Com base no `id` enviado, essa rota pode alterar um pedido, podendo ser um, ou todos os dados do pedido (exceto o `id` e o `status`, claro).

-   `PATCH /order/:id`: Com base no `id` enviado, assim que chamada, essa rota altera o status do pedido recebido para "Pronto".

-   `DELETE /order/:id`:  Com base no `id` enviado, assim que chamada, deleta o pedido recebido.

#### Exemplos
Ao chamar a rota `POST /order` passando `{ order: "X- Salada, 2 batatas grandes, 1 coca-cola", clienteName:"José", price: 44.50 }`, o array fica dessa forma:

```js
[
    {
        id: 'ac3ebf68-e0ad-4c1d-9822-ff1b849589a8',
        order: 'X- Salada, 2 batatas grandes, 1 coca-cola',
        clienteName: 'José',
        price: 44.5,
        status: 'Em preparação'
    }
];
```

Ao chamar a rota `PATCH /order/ac3ebf68-e0ad-4c1d-9822-ff1b849589a8`, o array fica dessa forma:

```js
[
    {
        id: 'ac3ebf68-e0ad-4c1d-9822-ff1b849589a8',
        order: 'X- Salada, 2 batatas grandes, 1 coca-cola',
        clienteName: 'José',
        price: 44.5,
        status: 'Pronto'
    }
];
```

### Middlewares
- `checkIdExistence`: Sua função é verificar se o ID recebido existe e tomar medidas em caso de inexistência. Ele é usado em todas as rotas que recebem um ID.

- `showMethodNUrl`: Sua função é mostrar no console o método(GET,POST,PUT,DELETE, etc) e também a url da requisição. Ele é usado em todas as requisições e tem o objetivo apenas de facilitar e organizar o desenvolvimento.

- `verifyClientData`: Sua função é verificar os dados do cliente enviados pelo `body`, e tomar medidas caso essa requisição tenha a intenção de modificar dados que o cliente não tem permissão.

## Como usar
Para clonar e executar este projeto, você precisará do [Git](https://git-scm.com/), [Node.js v16.13.2](https://nodejs.org/en/) ou superior, e de um API Client como o [Insomnia](https://insomnia.rest/) instalados em seu computador.<br>No terminal:

```bash
# Clone esse repositório:
$ git clone https://github.com/Luk4x/dev-burger-order-log-API.git

# Entre no repositório:
$ cd dev-burger-order-log-API

# Instalar dependências 
$ npm i

# Executar o projeto
$ npm run server

# O servidor irá iniciar em http://localhost:3000/, e você pode explorá-lo usando o Insomnia.
```

## Contato dos Contribuintes
<table>
  <tr>
    <td align="center">
      <a href="https://www.linkedin.com/in/lucasmacielf/">
        <img src="https://avatars.githubusercontent.com/Luk4x" width="150px;" alt="Luk4x Github Photo"/><br>
        <sub>
          <b>Lucas Maciel</b>
        </sub>
      </a>
    </td>
  </tr>
</table>
