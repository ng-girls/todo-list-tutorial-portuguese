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

Delegamos tudo ao componente pai - mesmo que altere o título do item, se necessário. \(O nome do método pode parecer irrelevante agora. Se você quiser, pode mudá-lo para algo mais apropriado, como `submitValue`. Lembre de mudar isso no template também.\)

Passamos `newTitle` quando emitimos o evento. O que quer que possamos passar em `emit ()` estará disponível para o pai como `$ event`.

Nada mais é alterado no componente todo-input. Os eventos emitidos por `keyup.enter` e` click` ainda chamam o mesmo método, mas o próprio método mudou.

Agora, tudo o que precisamos fazer é pegar o evento no componente principal e anexar lógica a ele. Vá para o componente app-root e vincule ao evento `submit` no componente `<todo-input>`:

```html
<todo-input (submit)="addItem($event)"></todo-input>
```

Agora tudo é deixado para implementar o método `addItem`, que recebe uma string e adiciona-a à lista:

```ts
addItem(title: string): void {    
  this.todoList.push({ title });
}
```

Teste!
