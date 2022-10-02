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
> Acesse o projeto online **[AQUI](https://luk4x-imanager-json-server.herokuapp.com/)**
<br>

## Tecnologias utilizadas
- [NodeJS](https://nodejs.org)
- [JSON-Server](https://yarnpkg.com/package/json-server)
- [Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

## Sobre
Esse projeto é uma JSON-Server API que realiza o cadastro de projetos e armazena as categorias de projetos de uma plataforma de gestão - a iManager, servindo como base para a sua [Interface](https://github.com/Luk4x/iManager) que desenvolvi essencialmente em [ReactJS](https://pt-br.reactjs.org).

### Rotas e Exemplos
-   `POST /projects`: Essa rota recebe o _nome do projeto_, o _orçamento do projeto_ e a _categoria do projeto_. Essas informações são passadas pelo `body` da requisição, e com base nelas um novo projeto é registrado dentro do array de projetos, no seguinte formato:
    
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

-   `PATCH /projects/:id`: Com base no `id` enviado e nos dados do projeto enviados pelo `body` da requisição, essa rota torna possível atualizar as informações de `name`, `budget` e/ou `category` de um projeto específico.<br/>
    Continuando do exemplo acima, ao chamar a rota `PATCH /projects/1` passando `{ name: "Novo Projeto 1", budget: 6500, category: { id: 2, name: "Desenvolvimento"} }`, o array ficará dessa forma:
    
     ```js
    [
        {
            "name": "Novo Projeto 1",
            "budget": "6500",
            "category": {
                "id": 2,
                "name": "Desenvolvimento"
            },
            "cost": 0,
            "services": [],
            "id": 1
        }
    ];
    ```
    
    Porém, através dessa rota também é possível atualizar o array de `services` do projeto, assim sendo possível Criar/Editar/Remover serviços - tudo dependerá do que estará sendo enviado pelo `body` da requisição. Tendo em mente que:<br/>
    
    ```js
        const project = {
            "name": "Novo Projeto 1",
            "budget": "6500",
            "category": {
                "id": 2,
                "name": "Desenvolvimento"
            },
            "cost": 0,
            "id": 1
        }
    ```
    
    Ao chamar a rota `PATCH /projects/1` passando `{...project, services: [ { name: "Contratação de Dev Front-End", cost: 3400, desc: "Responsável pelo desenvolvimento do layout da aplicação." } ] }`, o array ficará dessa forma:
    
    ```js
    [
        {
            "name": "Novo Projeto 1",
            "budget": "6500",
            "category": {
                "id": 2,
                "name": "Desenvolvimento"
            },
            "cost": 3400,
            "services": [
              {
                  "name": "Contratar Dev Front-End",
                  "cost": 3400,
                  "desc": "Responsável pelo desenvolvimento do layout da aplicação.",
                  "id": "dea206b3-409d-4b3f-9493-4bc2d27466a2"
              }
            ],
            "id": 1
        }
    ];
    ```

    O serviço que foi passado na requisição foi criado, e nesse caso, sua informação de `id` foi gerada pela biblioteca [uuid](https://www.uuidgenerator.net/).<br/>
    Para Editar/Deletar um serviço segue-se a mesma lógica: basta enviar um `project` no estado desejado na requisição, que através de seu `id`, ele substituirá o `project` existente no array de `projects`.<br/>
    Perceba que o valor de `cost` do projeto foi influenciado pelo serviço adicionado, isso porque o _custo do projeto_ está relacionado com seus _serviços_, portanto, se o projeto tiver 2 serviços com um `cost` de 4000 cada, logo, o `cost` do projeto será de 8000, porém, nesse caso é impossível disso acontecer, pois existem verificações para que o `cost` de um projeto não ultrapasse seu `budget`.
    
-   `DELETE /projects/:id`: Com base no `id` enviado, assim que chamada, essa rota deleta o projeto recebido.

-   `GET /categories`: Essa rota retorna todas as categorias existentes no array de `categories`.

## Como usar
Para clonar e executar este projeto, você precisará do [Git](https://git-scm.com/), [Node.js v16.13.2](https://nodejs.org/en/) ou superior, e de preferência, um API Client como o [Insomnia](https://insomnia.rest/) (mas também pode ser acessado pelo navegador) instalados em seu computador.<br>No terminal:

```bash
# Clone esse repositório com:
$ git clone https://github.com/Luk4x/iManager-json-server.git

# Entre no repositório com:
$ cd iManager-json-server

# Instale as dependências com: 
$ yarn install

# Execute o projeto com:
$ yarn start

# O servidor irá iniciar em http://localhost:5000/, e você pode explorá-lo usando o Insomnia ou um navegador.
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
