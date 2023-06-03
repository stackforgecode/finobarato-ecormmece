# App - o front-end da aplicação

Vamos criar a aplicação frontend com Angular para consumir os serviços da API que criamos com Laravel. Siga as etapas abaixo:

Etapa 1: Configuração do ambiente
Certifique-se de ter o Angular CLI instalado em seu sistema. Se você não tiver, instale-o executando o seguinte comando no terminal:

```
npm install -g @angular/cli
```

Etapa 2: Criação do projeto Angular
Abra o terminal e execute o seguinte comando para criar um novo projeto Angular:

```
ng new nome_do_projeto_frontend
```

Isso criará uma estrutura de diretórios básica para o projeto Angular.

Etapa 3: Configuração do serviço de API
Agora, vamos configurar o serviço de API no projeto Angular. Crie um novo serviço executando o seguinte comando no terminal:

```
ng generate service api
```

Isso criará um arquivo `api.service.ts` em `src/app` que você pode usar para fazer chamadas à API.

Abra o arquivo `api.service.ts` e substitua seu conteúdo pelo seguinte código de exemplo:

```typescript
import { Injectable } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class ApiService {
  private apiUrl = 'http://localhost:8000/api'; // Substitua pelo URL da sua API Laravel

  constructor(private http: HttpClient) { }

  private getHeaders(): HttpHeaders {
    const headersConfig = {
      'Content-Type': 'application/json',
      'Accept': 'application/json',
    };

    // Adicione aqui o token JWT para autenticar as chamadas à API, se necessário
    // headersConfig['Authorization'] = 'Bearer ' + token;

    return new HttpHeaders(headersConfig);
  }

  get(endpoint: string): Observable<any> {
    const url = `${this.apiUrl}/${endpoint}`;
    const headers = this.getHeaders();
    return this.http.get(url, { headers });
  }

  post(endpoint: string, data: any): Observable<any> {
    const url = `${this.apiUrl}/${endpoint}`;
    const headers = this.getHeaders();
    return this.http.post(url, data, { headers });
  }

  // Adicione métodos para PUT, PATCH e DELETE, se necessário
}
```

Certifique-se de substituir `http://localhost:8000/api` pelo URL da sua API Laravel.

Etapa 4: Implementação do componente
Agora, vamos implementar um componente para exibir os dados da API. Execute o seguinte comando no terminal para gerar um novo componente:

```
ng generate component produtos
```

Isso criará um componente chamado `produtos` com um arquivo `produtos.component.ts`.

Abra o arquivo `produtos.component.ts` e substitua seu conteúdo pelo seguinte código de exemplo:

```typescript
import { Component, OnInit } from '@angular/core';
import { ApiService } from '../api.service';

@Component({
  selector: 'app-produtos',
  templateUrl: './produtos.component.html',
  styleUrls: ['./produtos.component.css']
})
export class ProdutosComponent implements OnInit {
  produtos: any[] = [];

  constructor(private apiService: ApiService) { }

  ngOnInit(): void {
    this.apiService.get('produtos').subscribe(
      (response: any) => {
        this.produtos = response;
      },
      (error: any) => {
        console.error(error);
      }
    );
  }
}
```

Etapa 5: Exib

ição dos dados no template
Abra o arquivo `produtos.component.html` e substitua seu conteúdo pelo seguinte código de exemplo:

```html
<h2>Produtos</h2>
<ul>
  <li *ngFor="let produto of produtos">
    {{ produto.nome }}
  </li>
</ul>
```

Etapa 6: Configuração das rotas
Abra o arquivo `app-routing.module.ts` e defina uma rota para o componente `ProdutosComponent`. O arquivo deve ser semelhante ao seguinte código:

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { ProdutosComponent } from './produtos/produtos.component';

const routes: Routes = [
  { path: 'produtos', component: ProdutosComponent },
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

Etapa 7: Executando a aplicação
No terminal, navegue até o diretório do projeto frontend:

```
cd nome_do_projeto_frontend
```

Execute o seguinte comando para iniciar a aplicação Angular:

```
ng serve
```

Acesse `http://localhost:4200` no navegador e você verá a lista de produtos sendo exibida.

A partir deste ponto, você pode expandir a aplicação frontend adicionando mais componentes e recursos para consumir os outros endpoints da API.

Essas são as etapas básicas para criar a aplicação frontend com Angular para consumir a API Laravel. Lembre-se de adaptar o código às suas necessidades específicas e de consultar a documentação do Angular para obter mais informações sobre cada recurso.
