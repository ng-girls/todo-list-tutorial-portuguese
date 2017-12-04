# Adicionando itens

Queremos adicionar itens à nossa lista. Com Angular podemos fazer isso facilmente e ver o item adicionado imediatamente. Vamos fazer isso dentro do `inputComponent` que criamos antes. Vamos mudá-lo assim, ao pressionar a tecla Enter ou clicar no botão enviar, o valor da caixa de entrada se tornará o título do novo item. E o novo item será adicionado à lista.

Mas não queremos que o componente todo-input seja responsável por adicionar um novo item para a lista. Queremos que ele tenha uma responsabilidade mínima, e **delegue a ação em seu componente pai**. Uma das vantagens desta abordagem é que este componente será reutilizável e pode ser anexado a uma ação diferente em diferentes situações.

Por exemplo, no seu caso, poderemos usar o `inputComponent` dentro de `itemComponent`. Então, teremos uma caixa de entrada para cada item e poderemos editar o título do item. Neste caso, pressionar a tecla Enter ou o botão Salvar terá um efeito diferente.

Então, o que realmente queremos fazer é **emitir um evento** do componente todo-input sempre que o título for alterado. Com o Angular, podemos facilmente definir e emitir eventos de nossos componentes!

## @Output()

Dentro da classe `inputComponent` adicione a linha de código a seguir, que define uma saída para o componente.

```ts
@Output() submit: EventEmitter<string> = new EventEmitter();
```

A saída de propriedade será chamada de `submit`. Certifique-se de que Output e o EventEmitter foram adicionados à declaração de importação na primeira linha do arquivo:

```ts
import { Component, OnInit, Output, EventEmitter } from '@angular/core';
```

Agora, sempre que chamamos `this.submit.emit()` um evento será emitido para o componente pai. Vamos chamá-lo no método changeTitle:

```ts
changeTitle(newTitle: string): void {
  this.submit.emit(newTitle);
}
```

We delegate everything to the parent component - even actually changing the title of the item if needed. \(The method name may seem irrelevant right now. If you'd like you can change it to something more appropriate, such as `submitValue`. Remember to change it in the template as well.\)

We pass `newTitle` when we emit the event. Whatever we pass in `emit()` will be available for the parent as `$event`.

Nothing else is changed in the todo-input component. The events emitted from `keyup.enter` and `click` still call the same method, but the method itself has changed.

Now all we need to do is catch the event in the parent component and attach logic to it. Go to the app-root component and bind to the `submit` event in the `<todo-input>` component:

```html
<todo-input (submit)="addItem($event)"></todo-input>
```

Now all is left is to implement the `addItem` method, which receives a string and adds it to the list:

```ts
addItem(title: string): void {    
  this.todoList.push({ title });
}
```

Teste!
