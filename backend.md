# API - O back-end da aplicação

Vamos criar uma API usando o Laravel com os requisitos mencionados. Vamos dividir o processo em etapas.

Etapa 1: Configuração do ambiente
Certifique-se de que você tenha o Laravel instalado no seu sistema. Você pode instalar o Laravel executando o seguinte comando no terminal:

```
composer global require laravel/installer
```

Após a instalação, você pode criar um novo projeto Laravel usando o comando:

```
laravel new nome_do_projeto
```

Agora, vá para o diretório do projeto:

```
cd nome_do_projeto
```

Etapa 2: Configuração do banco de dados
Abra o arquivo `.env` na raiz do seu projeto Laravel e configure as informações de conexão com o banco de dados para os dois bancos de dados:

```
DB_CONNECTION=mysql
DB_HOST=seu_host
DB_PORT=3306
DB_DATABASE=auth_finobarato_db
DB_USERNAME=seu_usuario
DB_PASSWORD=sua_senha

DB_CONNECTION_SECONDARY=mysql
DB_HOST_SECONDARY=seu_host
DB_PORT_SECONDARY=3306
DB_DATABASE_SECONDARY=api_finobarato_db
DB_USERNAME_SECONDARY=seu_usuario
DB_PASSWORD_SECONDARY=sua_senha
```

Etapa 3: Criação das tabelas e autenticação JWT
Agora, vamos criar as tabelas necessárias e adicionar autenticação JWT à model User. Primeiro, execute os seguintes comandos para criar as migrações:

```
php artisan make:migration create_users_table --table=users --database=auth_finobarato_db
php artisan make:migration create_password_resets_table --table=password_resets --database=auth_finobarato_db
php artisan make:migration create_produtos_table --table=produtos --database=api_finobarato_db
php artisan make:migration create_categorias_table --table=categorias --database=api_finobarato_db
php artisan make:migration create_servicos_table --table=servicos --database=api_finobarato_db
php artisan make:migration create_vendas_table --table=vendas --database=api_finobarato_db
```

Agora, abra as migrações geradas em `database/migrations` e adicione os campos relevantes para cada tabela.

Em seguida, execute as migrações para criar as tabelas:

```
php artisan migrate --database=auth_finobarato_db
php artisan migrate --database=api_finobarato_db
```

Para adicionar autenticação JWT à model User, você precisará instalar o pacote JWT do Laravel. Execute o seguinte comando para instalá-lo:

```
composer require tymon/jwt-auth
```

Após a instalação, publique as configurações do pacote JWT:

```
php artisan vendor:publish --provider="Tymon\JWTAuth\Providers\LaravelServiceProvider"
```

Em seguida, gere a chave secreta para o JWT:

```
php artisan jwt:secret
```

Agora, abra o arquivo `config/auth.php` e defina o driver do guard `api` como JWT:

```php
'guards' => [
    'api' => [
        'driver' => 'jwt',
        'provider' => 'users',
    ],
],
```

Etapa 4: Criação das models
Agora, vamos criar as models para cada entidade do banco `api_finobarato_db`. Execute os seguintes comandos para criar as models:

``

`
php artisan make:model Produto --migration --controller --resource --database=api_finobarato_db
php artisan make:model Categoria --migration --controller --resource --database=api_finobarato_db
php artisan make:model Servico --migration --controller --resource --database=api_finobarato_db
php artisan make:model Venda --migration --controller --resource --database=api_finobarato_db
```

Isso criará as models, migrations, controllers e resource controllers para cada entidade.

Etapa 5: Definição das rotas
Abra o arquivo `routes/api.php` e defina as rotas para cada entidade. Por exemplo:

```php
Route::apiResource('produtos', 'ProdutoController');
Route::apiResource('categorias', 'CategoriaController');
Route::apiResource('servicos', 'ServicoController');
Route::apiResource('vendas', 'VendaController');
```

Etapa 6: Validação dos dados de entrada
Para cada entidade, você pode criar uma classe de validação para validar os dados de entrada. Por exemplo, para a entidade "Produto", execute o seguinte comando para criar uma classe de validação:

```
php artisan make:request StoreProdutoRequest
```

Abra o arquivo `app/Http/Requests/StoreProdutoRequest.php` e adicione as regras de validação necessárias.

Etapa 7: Implementação dos controllers
Abra os controllers gerados em `app/Http/Controllers` para cada entidade e implemente a lógica necessária para cada método, como index, store, update, etc.

Etapa 8: Testando a API
Agora, você pode testar a API usando um cliente HTTP, como o Postman ou o Insomnia. Certifique-se de incluir o token JWT nos cabeçalhos das solicitações autenticadas.

Essas são as etapas básicas para criar uma API com Laravel atendendo aos requisitos que você mencionou. Lembre-se de adaptar o código às suas necessidades específicas e de consultar a documentação do Laravel para obter mais informações sobre cada recurso.
