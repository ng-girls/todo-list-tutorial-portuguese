# Remover item

O usuário deverá ser capaz de remover qualquer item, independente de que o item esteja ativo ou de que já tenha sido completado.
A remoção de um item será feita a partir do click em um botão, apropriadamente chamado de 'remover'. 
Neste tutorial, iremos aprender como adicionar essa funcionalidade ao nosso projeto.

### Adicionando o botão "remover"
Primeiramente, precisamos adicionar o botão ao item, então iremos trabalhar no arquivo *todo-item.component.ts*.

Adicione um botão "remover" ao template do item, com um handler de click que chama o método *removeItem* (que iremos criar em breve):

{% code-tabs %} {% code-tabs-item title="src/app/todo-item/todo-item.component.ts" %}

```
template: `
  <div class="todo-item">
    {{ item.title }}

    <button class="btn btn-red" (click)="removeItem()">
      remove
    </button>
  </div>
`,
```
{% endcode-tabs-item %} {% endcode-tabs %}


Adicione uma nova saída à classe TodoItemComponent, que emitirá o item removido para o gerenciador de listas quando um usuário pressionar o botão remover: 

{% code-tabs %} {% code-tabs-item title="src/app/todo-item/todo-item.component.ts" %}
```
@Output() remove: EventEmitter<TodoItem> = new EventEmitter();
```
{% endcode-tabs-item %} {% endcode-tabs %}


Certifique-se de que importamos o EventEmitter e o Output em nossa classe:

{% code-tabs %} {% code-tabs-item title="src/app/todo-item/todo-item.component.ts" %}
```
import { Component, OnInit, Input, EventEmitter, Output } from '@angular/core';
```
{% endcode-tabs-item %} {% endcode-tabs %}


Adicione um método na classe ItemComponent que realmente irá emitir o evento. Esse método será chamado quando o usuário clicar no botão **remover**:

```
removeItem() {
  this.remove.emit(this.todoItem);
}
```

### Removendo o ToDo item

Agora que cada **ToDo item** pode emitir a sua própria remoção, vamos nos certificar de que o gerenciador da lista realmente remova este mesmo item da lista. Para isso, iremos trabalhar no arquivo *list-manager.component.ts*.

(a) Precisamos responder ao evento **remove** - vamos adicionar isso ao template, dentro da tag <todo-item>:

{% code-tabs %} {% code-tabs-item title="src/app/list-manager/list-manager.component.ts" %}
```
<app-todo-item [item]="todoItem"
               (remove)="removeItem($event)"></app-todo-item>
```
{% endcode-tabs-item %} {% endcode-tabs %}


(b) Agora só precisamos adicionar o método *removeItem()* à classe ListManagerComponent e usar o método *deleteItem*, do todoListService, que irá remover o item da lista e atualizará o armazenamento local:

{% code-tabs %} {% code-tabs-item title="src/app/list-manager/list-manager.component.ts" %}
```
removeItem(item) {
  this.todoListService.deleteItem(item);
}
```
{% endcode-tabs-item %} {% endcode-tabs %}

