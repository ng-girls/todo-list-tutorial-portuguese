# #13: 🚧 Refatorando o App Component

Vamos realizar uma pequena refatoração. O `app-root` não deve ter um tempalte tão grande e com toda essa lógica. Deve apenas chamar outro componente que irá lidar com isso.

* Crie um novo componente chamado `list-manager`:

`ng g c list-manager`

* Mova todo o código do `app-root` para `list-manager`.
* Você pode manter o título no `app-root`, e dar a ele um valor.
* Mas cuidado para não alterar o nome da classe do componente list manager!

{% code-tabs %} {% code-tabs-item title="src/app/app.component.ts" %}

```
  @Component({
    selector: 'app-root',
    template: `
      <h1>
        Welcome to {{ title }}!
      </h1>
    `,
    styleUrls: ['./app.component.css']
  })
  export class AppComponent {
    title = 'My To Do List APP'
  }
```
{% endcode-tabs-item %} {% endcode-tabs %}

{% code-tabs %} {% code-tabs-item title="src/app/list-manager/list-manager.component.ts" %}

```
  import { Component, OnInit } from '@angular/core';
  import { TodoItem } from '../interfaces/todo-item';
  
  @Component({
    selector: 'app-list-manager',
    template: `
      <app-input-button-unit (submit)="addItem($event)"></app-input-button-unit>
      
      <ul>
        <li *ngFor="let todoItem of todoList">
          <app-todo-item [item]="todoItem"></app-todo-item>
        </li>
      </ul>
    `,
    styleUrls: ['./list-manager.component.css']
  })
  export class ListManagerComponent implements OnInit {
    todoList: TodoItem[] = [
      {title: 'install NodeJs'},
      {title: 'install Angular CLI'},
      {title: 'create new app'},
      {title: 'serve app'},
      {title: 'develop app'},
      {title: 'deploy app'}
    ];
    
    constructor() { }
    
    ngOnInit() {
    }
    
    addItem(title: string) {
      this.todoList.push({ title })
    }
  }
```
{% endcode-tabs-item %} {% endcode-tabs %}

* Chame o novo componente no template do `app-root`:

{% code-tabs %} {% code-tabs-item title="src/app/app.component.ts" %}

```
  template: `
    <h1>
      Welcome to {{ title }}!
    </h1>
    
    <app-list-manager></app-list-manager>
    `,
```
{% endcode-tabs-item %} {% endcode-tabs %}

É isso! Agora podemos continuar.
