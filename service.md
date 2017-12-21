# Service

O que e por que
------------
Serviços são funções Javascript que são responsáveis somente por tarefas específicas. Serviços em Angular são injetados, usando um mecanismo de injeção de dependências e incluindo um valor, função ou feature necessária para aplicação. Em nosso ToDo app, nós vamos precisar de um serviço para salvar todas as tarefas e ele será utilizado via injeção de dependências nos componentes. 

Create
------------
In order to create a new service by **angular-cli**, we need to type this command on the root folder:

    ng g s todoList

This command will generate the service and put it under src/app/todo-list.service.ts

Criar
------------
Para criar um novo serviço com **angular-cli**, nós precisamos digitar o comando abaixo na raiz da pasta do seu projeto: 

    ng g s todoList

Este comando irá gerar o serviço e colocá-lo abaixo de src/app/todo-list.service.ts


Provisionando no ngModule 
------------

Agora, para começar a usar o serviço, primeiro precisamos provisioná-lo no componente @NgModule.
Em /src/app/app.module.ts, adicione um código de importação:

```javascript
import { TodoListService } from './todo-list.service';
```

E agora, adicione o serviço no array de "providers" e o componente ngModule ficará assim:


```javascript
@NgModule({
  declarations: [
    AppComponent,
    InputComponent,
    ItemComponent,
    ListManagerComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [TodoListService],
  bootstrap: [AppComponent]
})
```

Isso irá nos permitir criar uma instância do serviço e usá-la em qualquer lugar do nosso app.

Movendo a lista do componente para o serviço
------------
Agora, nós vamos mover o array todoList do componente para o nosso novo serviço. O serviço terá: 

```javascript
private todoList = [
    { title: 'install NodeJS' },
    { title: 'install Angular CLI' },
    { title: 'create new app' },
    { title: 'serve app' },
    { title: 'develop app' },
    { title: 'deploy app' },
  ];
```

Criando um método no serviço para retornar a lista
------------
Vá para o arquivo gerado para o serviço, que pode ser encontrado em src/app/todo-list.service.ts e adicione a função "getTodoList", que irá retornar o array todoList. O serviço ficará assim:

```javascript
import { Injectable } from '@angular/core';

@Injectable()
export class TodoListService {

  private todoList = [
    { title: 'install NodeJS' },
    { title: 'install Angular CLI' },
    { title: 'create new app' },
    { title: 'serve app' },
    { title: 'develop app' },
    { title: 'deploy app' },
  ];

  constructor() {
  }

  getTodoList() {
    return this.todoList;
  }
}
```

Injetando ao componente list-manager e utilizando o serviço
------------
Depois de criar uma instância para o serviço, precisamos intejar no nosso componente list-manager. Vá para o arquivo /src/app/list-manager/list-manager.component.ts e adicione o código de importação abaixo: 

```javascript
import { TodoListService } from '../todo-list.service'; 
```

Use isso somente na classe ListManagerComponent: Remova o array todoList, mas mantenha o todoList e altere o construtor para:

```javascript
constructor(private todoListService:TodoListService) { }
```

E, agora, o todoList irá utilizar o serviço que criamos na função **ngOnInit**:

```javascript
ngOnInit() {
    this.todoList = this.todoListService.getTodoList();
}
```

