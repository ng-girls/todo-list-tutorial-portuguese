# Remover item

O usurio deve ser capaz de remover qualquer item. Independente se o item ainda est ativo ou se já foi completado.
A remoção de um item será feita a partir de um click em um botão, apropriadamente chamado de 'Remover'. Neste tutorial, iremos aprender como adicionar essa funcionalidade ao nosso projeto.

### Arquivo: item.component.ts
Primeiramente, precisamos adicionar o botão ao item, então iremos trabalhar no arquivo *item.component.ts*.

(a) Adicione um evento de **(click)** ao botão **remover** no template do item.
```
<button (click)="removeItem()">
  remove
</button>
```

(b) Add a new output to the ItemComponent class, which will be emitted to the list manager when a user pressed the remove button for a specific item:
```
@Output() remove:EventEmitter<any> = new EventEmitter();
```

Make sure that we import both EventEmitter and Output in our class:
```
import { Component, OnInit, Input, EventEmitter, Output } from '@angular/core';
```
(c) Add a function to the ItemComponent class that will actually emit the event. This function will be called when the user clicks the **remove** button:
```
removeItem() {
  this.remove.emit(this.todoItem);
}
```

### File: list-manager.component.ts

Now that each todo item can emit its own removal, let's make sure that the list manager actually removes that same item from the list. For that, we'll work on the file *list-manager.component.ts*.

(a) We need to respond to **remove** event - let's add it to the template, inside the `<todo-item>` tag:
```
(remove)="removeItem($event)"
```

(b) Now we just need to add the function *removeItem()* to the ListManagerComponent class:
```
removeItem(item) {
  this.todoList = this.todoListService.removeItem(item);
}
```

### File: todo-list.service.ts

Removing the item is handled in the service - open *todo-list.service.ts* and add a function called removeItem() to the TodoListService class:

```
removeItem(item) {
  return this.storage.destroy(item);
}
```

This function calls the destroy() method we already created in  todo-list-storage.service.ts earlier.
