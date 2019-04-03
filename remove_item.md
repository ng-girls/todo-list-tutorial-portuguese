# Remover item

O usuário deve ser capaz de remover qualquer item. Independente se o item ainda está ativo ou se já foi completado.
A remoção de um item será feita a partir de um click em um botão, apropriadamente chamado de 'Remover'. Neste tutorial, iremos aprender como adicionar essa funcionalidade ao nosso projeto.

### Arquivo: item.component.ts
Primeiramente, precisamos adicionar o botão ao item, então iremos trabalhar no arquivo *item.component.ts*.

(a) Adicione um evento de **(click)** ao botão **remover** no template do item.
```
<button (click)="removeItem()">
  remove
</button>
```

(b) Adicione uma nova saída **(emissor de evento / Output)** na classe ItemComponent, que será emitida para o gerenciador da lista quando um usuário clicar no botão remover de um item específico.
```
@Output() remove:EventEmitter<any> = new EventEmitter();
```

Certifique-se de que importamos o EventEmitter e o Output em nossa classe:
```
import { Component, OnInit, Input, EventEmitter, Output } from '@angular/core';
```
(c) Adicione uma função a classe ItemComponent que realmente irá emitir o evento. Essa função será chamada quando o usuário clicar no botão **remover**:
```
removeItem() {
  this.remove.emit(this.todoItem);
}
```

### Arquivo: list-manager.component.ts

Agora que cada **ToDo item** pode emitir a sua própria remoção, vamos nos certificar de que o gerenciador da lista realmente remova este mesmo item da lista. Para isso, iremos trabalhar no arquivo *list-manager.component.ts*.

(a) Precisamos responder ao evento **remove** - vamos adicionar isso ao template, dentro da tag <todo-item>:
```
(remove)="removeItem($event)"
```
(b) Agora só precisamos adicionar a função *removeItem()* a classe ListManagerComponent:
```
removeItem(item) {
  this.todoList = this.todoListService.removeItem(item);
}
```

### Arquivo: todo-list.service.ts
A remoção do item é tratada no ```service``` - abra o arquivo *todo-list.service.ts* e adicione uma função chamada removeItem() a classe TodoListService:
```
removeItem(item) {
  return this.storage.destroy(item);
}
```
Essa função chama o método destroy() que já criamos em um momento anterior no arquivo **todo-list-storage.service.ts**.
