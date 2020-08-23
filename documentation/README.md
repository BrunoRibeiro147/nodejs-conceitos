# Conceitos do Node

## O que é o Node.js?

- Javascript no back-end;
  - Não lidamos com eventos do usuário final;
  - Rotas e integrações;
- Plataforma (não linguagem);
- Construída em cima da V8;
- Comparável a PHP / Ruby / Python / Go;

## O que é o NPM?

- Instalar bibliotecas de terceiros;
- Fornecer bibiotecas;
- Por que utilizaremos o Yarn?
  - Ele está avançando mais rápido que o NPM em questão de funcionalidades;
- Comparáveis:
  - Composer do PHP;
  - Gems do Ruby;
  - PIP do Python;

## Características do Node

- Arquitetura Event-loop;
  - Baseada em eventos (Rotas na maioria das vezes);
  - Call Stack;
- Node single-thread;
- C++ por trás com libuv;
- Background threads;
- Non-blocking I/O;

<p align="center">
  <img src="../readme/call-stack.png" width="404" height="416">
</p>

## Frameworks

- ExpressJS como base:
  - Sem opinião;
  - Ótimo para iniciar;
  - Micro-serviços;
- Frameworks opinados:
  - AdonisJS;
  - NestJS;

# Conceitos API REST

## Como funciona?

- Fluxo da requisição e resposta:
  - Requisição feira por um cliente;
  - Resposta retornada através de uma estrutura de dados;
  - Cliente recebe resposta e processa resultado;
  - As rotas utilizam métodos HTTP:
    - <span style="color: #75f3d0;">GET</span> http://minhaapi.com/<span style="color: #BB227B;">users</span>
    - <span style="color: #75f3d0;">POST</span> http://minhaapi.com/<span style="color: #BB227B;">users</span>
    - <span style="color: #75f3d0;">PUT</span> http://minhaapi.com/<span style="color: #BB227B;">users</span>/<span style="color: #EDBE00;">1</span>
    - <span style="color: #75f3d0;">DELETE</span> http://minhaapi.com/<span style="color: #BB227B;">users</span>/<span style="color: #EDBE00;">1</span>

<p align="center">
  <img src="../readme/routes-resources.png">
</p>

## Benefícios

- Múltiplos clientes (front-end), mesmo back-end;
- Protocolo de comunicação padronizado (JSON);
  - Mesma estrutura para web / mobile / API pública;
  - Comunicação com serviços externos;

## Conteúdo da requisição

<p align="center">
  <img src="../readme/request-content.png" width="572" height="232">
</p>

## HTTP Codes

- <span style="color: #5097C2;">1xx</span>: Informational
- <span style="color: #489C8E;">2xx: Success
  - 200: SUCCESS
  - 201: CREATED
- <span style="color: #AD4A81;">3xx</span>: Redirection
  - 301: MOVED PERMANENTLY
  - 302: MOVED
- <span style="color: #E4C547;">4xx</span>: Client Error
  - 400: BAD REQUEST
  - 401: UNAUTHORIZED
  - 404: NOT FOUND
- <span style="color: #EF6E64;">5xx</span>: Server Error
  - 500: INTERNAL SERVER ERROR

> 💡 BORA CODAR!

# Criando projeto Node

- Criar pasta para o projeto;
- Navegar até a pasta no terminal;
- Executar `yarn init -y` para iniciar o projeto;
  - O comando acima vai criar o `package.json` , um arquivo que guarda algumas informações sobre o projeto;
- Abrir o projeto no VS Code com `code .`;
  - Caso não tenha o comando `code .` reconhecido no terminal:
    - Abra uma janela do VS Code;
    - Aperte `Ctrl` + `Shift` + `P` (ou `Cmd` + `Shift` + `P` );
    - Pesquise e selecione a opção: `Install 'code' command in PATH` ;
- Crie uma pasta `src` dentro do projeto;
- Dentro da `src` crie um `index.js` ;
- No terminal execute `yarn add express` para instalar o Express;
- No arquivo `index.js` insira o código:

```jsx
// Importa o Express instalado
const express = require('express');

// Cria uma instância do Express
const app = express();

// Cria uma rota acessível pelo método GET e com o endereço /projects
app.get('/projects', (request, response) => {
  // Retorna para o cliente uma mensagem em formato de texto
  return response.send('Hello World');
});

// Define que a aplicação vai rodar na porta 3333, por exemplo:
// http://localhost:3333
app.listen(3333);
```

- Para executar o código, execute no terminal: `node src/index.js` ;
- Abra o Browser e acesse: `http://localhost:3333/projects` ;
- Modifique o `/projects` para `/` para poder acessar com o endereço `http://localhost:3333` ;
- Troque o `.send('Hello World')` por `.json({ message: 'Hello World' })` para que o retorno seja sempre no padrão JSON;
- Para ver o funcionamento, pare a execução no terminal com `Ctrl` + `C` e execute novamente `node src/index.js` ;
- Para finalizar acesse `http://localhost:3333` e veja o resultado;
- Não usamos o `request` da rota pois é nele onde ficam armazenadas as informações da rota acessada, tal como os dados enviados pelo usuário, veremos como fazer uso dela nas próximas aulas;

# Configurando Nodemon

- O Nodemon é uma ferramenta utilizada por toda comunidade Node para fazer a atualização automática do servidor quando o Node detectar uma  alteração no código;
- Instalar o Nodemon executando `yarn add nodemon -D` para instalar como dependência de desenvolvimento;
- Há 2 maneiras de se executar o Nodemon;
  - A primeira e mais comum é executando no terminal `nodemon src/index.js` no terminal;
  - A segunda maneira é:
    - Criar um índice `scripts` no `package.json`;
    - Dentro do `scripts` inserir o índice `"dev": "nodemon"`;
    - No índice `main` modificar o valor para ficar: `"main": "src/index.js"`;
    - Executar no terminal `yarn dev`;
- Modificar a `message` de `Hello World` para `Hello GoStack` e salvar para ver o resultado;
- Adicionar uma arrow function no segundo parâmetro da função `app.listen` para que uma mensagem seja disparada automaticamente sempre que o servidor for reiniciado, ficando dessa forma:
  ```javascript
  app.listen(3333, () => {
    console.log('🚀 Back-end started!');
  });
  ```
- Ao salvar o arquivo o resultado deve ser aparente no terminal, com o servidor reiniciando automaticamente;

# Métodos HTTP

- Métodos HTTP:
  - GET: Buscar informações do Back-end;
  - POST: Criar uma informação no Back-end;
  - PUT/PATCH: Alterar uma informação no Back-end;
  - DELETE: Deletar uma informação no Back-end;
- Criar 4 rotas novas, uma com cada método;
  - Modificar a rota já criada com o método GET para ficar como abaixo:
    ```javascript
    app.get('/projects', (request, response) => {
      return response.json([
        'Projeto 1',
        'Projeto 2',
      ]);
    });
    ```
  - Criar uma nova rota com método POST com o código:
    ```javascript
    app.post('/projects', (request, response) => {
      return response.json([
        'Projeto 1',
        'Projeto 2',
        'Projeto 3',
      ]);
    });
    ```
    - Rotas com método POST não podem ser testadas diretamente no navegador sem ser feito uma "gambiarra";
  - Criar uma nova rota com o método PUT com o código:
    ```javascript
    app.put('/projects/:id', (request, response) => {
      return response.json([
        'Projeto 4',
        'Projeto 2',
        'Projeto 3',
      ]);
    });
    ```
    - O `:id` na rota indica que é um parâmetro que vai ser passado na chamada daquela rota;
    - Rotas com método PUT também não podem ser testadas diretamente no navegador;
  - Criar uma nova rota com o método DELETE com o código:
    ```javascript
    app.delete('/projects/:id', (request, response) => {
      return response.json([
        'Projeto 2',
        'Projeto 3',
      ]);
    });
    ```
    - O `:id` na rota indica que é um parâmetro que vai ser passado na chamada daquela rota;
    - Rotas com método DELETE também não podem ser testadas diretamente no navegador;

# Utilizando Insomnia

- Acessar, baixar e instalar o Insomnia ([https://insomnia.rest](https://insomnia.rest/));
- Instalar o Tema Dracula para o Insomnia ([https://draculatheme.com/insomnia/](https://draculatheme.com/insomnia/));
- Criar um novo `Workspace`;

<p align="center">
  <img src="../readme/create-workspace.png" width="641" height="527">
</p>

- Criar um `Folder` para cada tipo de recurso, inicialmente criar um para `Projects`;

<p align="center">
  <img src="../readme/create-folder.png" width="641" height="527">
</p>

- Criar uma `Request` dentro da Folder, clicando em `click to add first request...` , dar o nome de `List` e manter o método `GET`;

<p align="center">
  <img src="../readme/create-request.png" width="641" height="527">
</p>

- Inserir na barra de endereço a URL da aplicação Node e dar um `Send`;

<p align="center">
  <img src="../readme/send-request.png" width="641" height="527">
</p>

- O retorno deve ser igual ao retorno do browser;
- Duplicar a rota criada anteriormente e mudar o método para `POST` e o nome para `Create`, feito isso dar um `Send` novamente;

<p align="center">
  <img src="../readme/duplicate-request.png" width="641" height="527">
</p>

- Duplicar novamente a rota e mudar o método para `PUT` e o nome para `Update` , ao tentar enviar vai ocorrer um erro, pois essa rota espera um `id` como parâmetro, basta inserir ao final da URL da aplicação o seguinte: `/1` e dar um `Send`;

<p align="center">
  <img src="../readme/put-request.png" width="641" height="527">
</p>

- Duplicar a rota `Update` , mudar apenas o método para `Delete` e dar um `Send` novamente;
- Criar um novo `Environment`;

<p align="center">
  <img src="../readme/create-environment.png" width="641" height="527">
</p>

  - Os `Environments` são usados para separar as rotas para testar a aplicação local e também online;
- Criar um `Sub Environment` com nome `dev` ;

<p align="center">
  <img src="../readme/create-sub-environment.png" width="641" height="527">
</p>

  - Pra renomear o `Sub Environment` criado basta dar 2 cliques sobre o nome;
- Criar a variável `base_url` no `Sub Environment` criado, ficando assim:
  ```json
  {
    "base_url": "http://localhost:3333"
  }
  ```
- Clicar em `Done` para salvar o `Environment`;
- Clicar no aviso `No Environment` e selecionar o `dev` criado anteriormente;

<p align="center">
  <img src="../readme/select-environment.png" width="641" height="527">
</p>

- Trocar nas rotas criadas a URL `http://localhost:3333` por `base_url`;

<p align="center">
  <img src="../readme/change-url.png" width="641" height="527">
</p>

  - Ao começar a digitar `base_url` o Insomnia irá sugerir a variável criada no `Environment`;

# Tipos de Parâmetros

## Tipos de Parâmetros

- Query Params: Filtros e paginação;
  - Passado através das URL:
    ```
    http://localhost:3333/projects?title=React&owner=Diego
    ```
  - No Insomnia há uma aba específica para isso:

<p align="center">
  <img src="../readme/query-params.png" width="641" height="527">
</p>

- Route Params: Identificar recursos (Atualizar/Deletar);
  - Passado através da URL:
    ```
      http://localhost:3333/projects/1
    ```
    - Esse tipo de parâmetro já foi usado nas rotas com os métodos `PUT` e `DELETE` para passar o id;
- Request Body:Conteúdo na hora de criar ou editar um recurso (JSON);
  - No Insomnia há como inserir um corpo na requisição:
  - Inserir no Body da requisição `Create` no Insomnia o seguinte conteúdo:
    ```json
    {
      "title": "Aplicativo React Native",
      "owner": "Diego Fernandes"
    }
    ```

## Modificando a aplicação

- Inserir na rota `/projects` com método `GET` o código abaixo:
  ```jsx
  app.get('/projects', (request, response) => {
    // Recupera do request.query as variáveis title e owner
    const { title, owner } = request.query;

    // Printa no terminal as variáveis recuperadas;
    console.log(title);
    console.log(owner);

    // ...
  });
  ```
- Inserir na rota `/projects/:id` com método `PUT` o código abaixo:
  ```jsx
  app.put('/projects/:id', (request, response) => {
    // Recupera do request.params a variável id
    const { id } = request.params;

    // Printa no terminal a variável recuperada
    console.log(id);

    // ...
  });
  ```
- Adicionar o Middleware do Express para entender o formato do Body como JSON:
  - Inserir logo no começo do arquivo `index.js` o seguinte:
    ```jsx
    import express from 'express';

    const app = express();

    // Middleware que vai garantir o parse do request.body para JSON
    app.use(express.json());

    // ...
    ```
- Inserir na rota `/projects` com método `POST` o código abaixo:
  ```jsx
  app.post('/projects', (request, response) => {
    // Recupera do request.body as variáveis title e owner
    const { title, owner } = request.body;

    // Printa no terminal as variáveis recuperadas;
    console.log(title);
    console.log(owner);

    // ...
  });
  ```
