<p align="center">
  <a href="http://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo-small.svg" width="200" alt="Nest Logo" /></a>
</p>

[circleci-image]: https://img.shields.io/circleci/build/github/nestjs/nest/master?token=abc123def456
[circleci-url]: https://circleci.com/gh/nestjs/nest

  <p align="center">A progressive <a href="http://nodejs.org" target="_blank">Node.js</a> framework for building efficient and scalable server-side applications.</p>
    <p align="center">
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/v/@nestjs/core.svg" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/l/@nestjs/core.svg" alt="Package License" /></a>
<a href="https://www.npmjs.com/~nestjscore" target="_blank"><img src="https://img.shields.io/npm/dm/@nestjs/common.svg" alt="NPM Downloads" /></a>
<a href="https://circleci.com/gh/nestjs/nest" target="_blank"><img src="https://img.shields.io/circleci/build/github/nestjs/nest/master" alt="CircleCI" /></a>
<a href="https://coveralls.io/github/nestjs/nest?branch=master" target="_blank"><img src="https://coveralls.io/repos/github/nestjs/nest/badge.svg?branch=master#9" alt="Coverage" /></a>
<a href="https://discord.gg/G7Qnnhy" target="_blank"><img src="https://img.shields.io/badge/discord-online-brightgreen.svg" alt="Discord"/></a>
<a href="https://opencollective.com/nest#backer" target="_blank"><img src="https://opencollective.com/nest/backers/badge.svg" alt="Backers on Open Collective" /></a>
<a href="https://opencollective.com/nest#sponsor" target="_blank"><img src="https://opencollective.com/nest/sponsors/badge.svg" alt="Sponsors on Open Collective" /></a>
  <a href="https://paypal.me/kamilmysliwiec" target="_blank"><img src="https://img.shields.io/badge/Donate-PayPal-ff3f59.svg"/></a>
    <a href="https://opencollective.com/nest#sponsor"  target="_blank"><img src="https://img.shields.io/badge/Support%20us-Open%20Collective-41B883.svg" alt="Support us"></a>
  <a href="https://twitter.com/nestframework" target="_blank"><img src="https://img.shields.io/twitter/follow/nestframework.svg?style=social&label=Follow"></a>
</p>
  <!--[![Backers on Open Collective](https://opencollective.com/nest/backers/badge.svg)](https://opencollective.com/nest#backer)
  [![Sponsors on Open Collective](https://opencollective.com/nest/sponsors/badge.svg)](https://opencollective.com/nest#sponsor)-->

## Descrição

Trata-se de uma construção de uma API REST de back-end para um aplicativo de blog chamado "Median" (um clone simples do Medium). É utilizado framkework [Nest](https://github.com/nestjs/nest) no projeto, sendo iniciado  um servidor PostgreSQL conectando-se ao Prisma. Por fim, a API REST é documentada com Swagger.

## Tecnologias usadas

* `NestJS` como backend framework
* `Prisma` como Object-Relational Mapper (ORM)
* `PostgreSQL` como banco de dados
* `Swagger` como ferramenta API de documentação
* `TypeScript` como linguagem de programação
* `Docker` como container para rodar a aplicação
* `Node.js` v20.3.1

## Instalação do projeto

```bash
# ir até o caminho/path do projeto
$ cd nestjs-prisma-blog-api

# instalar dependências do projeto
$ npm install

# inicializar o database PostgreSQL com docker
$ docker-compose up -d

# aplicar a migrations do database
$ npx prisma migrate dev

# inicializar o projeto
$ npm run start:dev
```
Estrutura do projeto:
```
nestjs-prisma-blog-api
  ├── node_modules
  ├── prisma
  │   ├── migrations
  │   ├── schema.prisma
  │   └── seed.ts
  ├── src
  │   ├── app.controller.spec.ts
  │   ├── app.controller.ts
  │   ├── app.module.ts
  │   ├── app.service.ts
  │   ├── main.ts
  │   ├── articles
  │   └── prisma
  ├── test
  │   ├── app.e2e-spec.ts
  │   └── jest-e2e.json
  ├── README.md
  ├── .env
  ├── docker-compose.yml
  ├── nest-cli.json
  ├── package-lock.json
  ├── package.json
  ├── tsconfig.build.json
  └── tsconfig.json
```
Os arquivos e diretórios são:

* A pasta `src` contém o código da aplicação. Nela há os módulos:
  * O módulo `app` está situado na raiz do diretório src e é o *entrypoint* do aplicativo. É responsável por iniciar o servidor web.
  * O módulo `prisma` possui o Prisma Client, seu construtor de consultas do database.
  * O módulo `articles` definie os *endpoints* para a rota `/articles` e lógica de negócio que acompanha.
* O módulo `prisma` possui:
  * O arquivo `schema.prisma` que define o database schema.
  * A pasta `migrations` que contém o histórico de migration do database.
  * O arquivo `seed.ts` contém script para propagar/carregar o database de desenvolvimento com dados fictícios.
* O `docker-compose.yml`, arquivo que define a imagem Docker para uso do banco PostgreSQL.
* Arquivo `.env` que contém variáveis de ambiente, como conexão com o database PostgreSQL.

## Como rodar a API

```bash
# development
$ npm run start

# watch mode
$ npm run start:dev

# production mode
$ npm run start:prod
```
Assim, a documentação da API pode ser acessada pela URL `http://localhost:3000/api`

## Teste

```bash
# unit tests
$ npm run test

# e2e tests
$ npm run test:e2e

# test coverage
$ npm run test:cov
```
## Tratamento de erros de persistência

Utilizou-se um filtro de exceções para captura de erros do Prisma com objetivo de retornar o HTTP Status adequado. A criação foi através do comando:

- `npx nest generate filter prisma-client-exception`

Assim, a classe `PrismaClientExceptionFilter` foi modificada estendendo `BaseExceptionFilter` de `@nestjs/core`.

- Catálogo de códigos de erros capturados por `PrismaClientKnownRequestError` - [Prisma / ORM / Reference / Error message reference](https://www.prisma.io/docs/orm/reference/error-reference)

## Endpoints

Os *endpoints REST* podem ser visualizados através do swagger, pela URL `http://localhost:3000/api` configurada na implementação de `src/main.ts`.

## Referências

- Author - [Kamil Myśliwiec](https://kamilmysliwiec.com)
- Website - [https://nestjs.com](https://nestjs.com/)
- Twitter - [@nestframework](https://twitter.com/nestframework)
