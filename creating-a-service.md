# \#15:  🔋 Criar um Serviço

No Angular, um Serviço é \(tipicamente\) uma classe Javascript cuja responsabilidade é executar uma tarefa específica necessária à sua aplicação. Em nossa aplicação *to-do list*, nós iremos criar um serviço que será responsável por salvar e gerenciar todas as tarefas, e usaremos esse serviço injetando-o nos componentes.

## Criar um serviço com Angular CLI:

```text
ng g s services/todo-list
```

Este comando irá gerar o serviço no arquivo `src/app/services/todo-list.service.ts`. O serviço é simplesmente uma classe Javascript chamada `TodoListService`. Ela possui o *decorator* `@Injectable` que permite usar a Injeção de Dependência.

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```text
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class TodoListService {

  constructor() { }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Prover o serviço

Na versão 6 do Angular CLI você não precisa mais prover o serviço por conta própria - o CLI adiciona-o à raiz `NgModule`. Mas você pode continuar lendo para entender o que acontece e o que isso significa.

Para começar a usar o serviço, primeiro precisamos provê-lo ao `NgModule`. Nós temos apenas um `NgModule` na nossa aplicação - o `AppModule` localizado em `/src/app/app.module.ts`. Ele é uma classe vazia precedida pelo *decorator* `@NgModule` o qual passamos um objeto de configuração. Uma das propriedades desse objeto é uma lista de `providers` que está atualmente vazia. Nós adicionaremos nosso novo serviço à esta lista.

{% code-tabs %}
{% code-tabs-item title="src/app/app.module.ts" %}
```typescript
@NgModule({
  declarations: [
    AppComponent,
    InputButtonUnitComponent,
    TodoItemComponent,
    ListManagerComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [TodoListService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

O array de `providers` diz ao Angular como prover um serviço que estamos procurando \(normalmente em um componente ou outro serviço\). Nesse momento a receita é simples: Quando nós pedimos pela classe `TodoListComponent` nós esperamos obter uma instância dessa classe. O Angular criará apenas uma instância que nós podemos acessar de qualquer lugar da nossa aplicação \(um Singleton\), então nós podemos usá-la para compartilhar dados entre diferentes partes da aplicação

Certifique-se que o serviço está importado:

{% code-tabs %}
{% code-tabs-item title="src/app/app.module.ts" %}
```typescript
import { TodoListService } from './services/todo-list.service';
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Compartilhar dados

Agora nós podemos mover o array `todoList` do `ListManagerComponent` para o nosso novo serviço. Abra o arquivo do serviço gerado, `src/app/services/todo-list.service.ts`, e adicione este código dentro da classe `TodoListService` logo abaixo do `constructor`:

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
private todoList: TodoItem[] = [  {title: 'install NodeJS'},
  {title: 'install Angular CLI'},
  {title: 'create new app'},
  {title: 'serve app'},
  {title: 'develop app'},
  {title: 'deploy app'},
];
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Tenha certeza de que a interface TodoItem está importada:

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
import { TodoItem } from '../interfaces/todo-item';
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Criar um método para retornar a lista

Nós adicionaremos o método `getTodoList` que retornará o array `todoList`. O serviço ficará assim:

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
import { Injectable } from '@angular/core';
import { TodoItem } from '../interfaces/todo-item';

@Injectable({
  providedIn: 'root'
})
export class TodoListService {

  private todoList: TodoItem[] = [
    {title: 'install NodeJS'},
    {title: 'install Angular CLI'},
    {title: 'create new app'},
    {title: 'serve app'},
    {title: 'develop app'},
    {title: 'deploy app'},
  ];

  constructor() { }

  getTodoList() {
    return this.todoList;
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Injetar e usar o serviço

Depois de criar o serviço, nós podemos injetá-lo no nosso componente `list-manager`. Na Injeção de Dependência do Angular isso é muito simples. Nós o passamos como um parâmetro no construtor - o tipo do parâmetro é o nome da classe do serviço. O Angular atribui a instância criada ao nome do parâmetro e nós podemos usá-lo a partir do construtor. Antes de implementarmos por nós mesmos, vamos ver como isso funciona: 

```typescript
constructor(todoListService: TodoListService) {
  todoListService.getTodoList();
}
```

O Typescript nos ajuda ainda mais nos fornecendo um atalho para atribuir o parâmetro a um membro de classe. Adicionando `private` ou `public` antes do nome do parâmetro ele é automaticamente atribuído ao `this`. Então, em vez de declarar e atribuir a propriedade por nós mesmos: 

```typescript
export class ListManagerComponent implements OnInit {
  todoListService: TodoListService;
  
  constructor(todoListService:TodoListService) { 
    this.todoListService = todoListService;
  }
}
```

...nós podemos reduzir muito código da seguinte forma:

```typescript
export class ListManagerComponent implements OnInit {
  
  constructor(private todoListService:TodoListService) { }
}
```

Então vamos continuar e usar o serviço no componente `list-manager`.

* Remova a lista codificada do componente e mantenha apenas a declaração de propriedade `todoList`.
* Injete o `TodoListService` usando o construtor.

```typescript
export class ListManagerComponent implements OnInit {
  todoList: TodoItem[];
  
  constructor(private todoListService:TodoListService) { }
```

* Certifique-se que `TodoListService` está importado.

{% code-tabs %}
{% code-tabs-item title="src/app/list-manager/list-manager.component.ts" %}
```typescript
import { TodoListService } from '../services/todo-list.service';
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Obtenha a lista do serviço no método `ngOnInit`.

{% code-tabs %}
{% code-tabs-item title="src/app/list-manager/list-manager.component.ts" %}
```typescript
ngOnInit() {
  this.todoList = this.todoListService.getTodoList();
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Você não precisa alterar nada no modelo uma vez que estamos atribuindo a lista à mesma propriedade que usamos antes. Parece que nada mudou, mas você pode verificar que a lista vem do serviço mudando de lá \(adicionando um item, trocando o título, etc.\) .
