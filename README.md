# Finobarato Loja Virtual

![GitHub](https://img.shields.io/github/license/stackforgecode/finobarato-ecommerce)
![GitHub repo size](https://img.shields.io/github/repo-size/stackforgecode/finobarato-ecommerce)
![GitHub last commit](https://img.shields.io/github/last-commit/stackforgecode/finobarato-ecommerce)

## Descrição

Finobarato Loja Virtual é um projeto de comércio eletrônico (e-commerce) desenvolvido com Laravel e Angular. O projeto consiste em uma API Laravel para gerenciar produtos, categorias, serviços e vendas, e um aplicativo Angular para consumir essa API e fornecer uma interface de usuário para os clientes.

## Recursos

- Autenticação de usuário com JWT usando Laravel
- Gerenciamento de produtos, categorias, serviços e vendas
- Interface de usuário interativa com Angular
- Integração com banco de dados MySQL

## Requisitos do Sistema

- PHP >= 7.2
- Composer
- Laravel >= 8.x
- Angular CLI
- Node.js
- MySQL >= 5.7

## Instalação

### API Laravel

1. Clone este repositório: `git clone https://github.com/stackforgecode/finobarato-ecommerce.git`
2. Navegue até o diretório `api`: `cd finobarato-ecommerce/api`
3. Instale as dependências do Laravel: `composer install`
4. Configure as variáveis de ambiente no arquivo `.env` (consulte o exemplo no arquivo `.env.example`)
5. Execute as migrações para criar as tabelas do banco de dados: `php artisan migrate`

### Aplicativo Angular

1. Navegue até o diretório `app`: `cd finobarato-ecommerce/app`
2. Instale as dependências do Angular: `npm install`
3. Execute a aplicação Angular: `ng serve`

### Scripts do Banco de Dados

- Os scripts SQL para a criação das tabelas e inserção de dados estão localizados no diretório `scripts-db`.

## Autor

- Nome: Rubens Lyra
- GitHub: [@stackforgecode](https://github.com/stackforgecode)
- Canal do YouTube: [StackForge](https://youtube.com/StackForge)

## Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir uma issue ou enviar um pull request.

## Licença

Este projeto está licenciado sob a [Licença MIT](LICENSE).
