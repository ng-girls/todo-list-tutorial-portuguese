# \#12: 📌Adicionando itens

Queremos adicionar itens à nossa lista. Com Angular podemos fazer isso facilmente e ver o item adicionado imediatamente. Vamos fazer isso dentro do `input-button-unit` que criamos antes. Vamos mudá-lo assim, ao pressionar a tecla Enter ou clicar no botão enviar, o valor da caixa de entrada se tornará o título do novo item. E o novo item será adicionado à lista.

Mas não queremos que o componente `input-button-unit` seja responsável por adicionar um novo item para a lista. Queremos que ele tenha uma responsabilidade mínima, e **delegue a ação em seu componente pai**. Uma das vantagens desta abordagem é que este componente será reutilizável e pode ser anexado a uma ação diferente em diferentes situações.

Por exemplo, no seu caso, poderemos usar o `input-button-unit` dentro do componente `todo-item`. Então, teremos uma caixa de entrada para cada item e poderemos editar o título do item. Neste caso, pressionar a tecla Enter ou o botão Salvar terá um efeito diferente.

Então, o que realmente queremos fazer é **emitir um evento** do componente `input-button-unit` sempre que o título for alterado. Com o Angular, podemos facilmente definir e emitir eventos de nossos componentes!

## @Output()

Dentro da classe `InputButtonUnitComponent` adicione a linha de código a seguir, que define uma saída para o componente.

```ts
@Output() submit: EventEmitter<string> = new EventEmitter();
```

A propriedade de saída será chamada de `submit`. Ela será do tipo `EventEmitter` que possui o método `emit`. `EventEmitter` é um tipo genérico(Generic Type) - nós passamos outro tipo que poderá ser utilizado internamente, nesse caso será uma `string`. É o tipo do objeto que será emitido pelo método `emit`.
  
Certifique-se de que Output e o EventEmitter foram adicionados à declaração de importação na primeira linha do arquivo:

```ts
import { Component, OnInit, Output, EventEmitter } from '@angular/core';
```

Agora, sempre que chamamos `this.submit.emit()` um evento será emitido para o componente pai. Vamos chamá-lo no método changeTitle:

```ts
changeTitle(newTitle: string): void {
  this.submit.emit(newTitle);
}
```

Delegamos tudo ao componente pai - mesmo que altere o título do item, se necessário.  
  
Passamos `newTitle` quando emitimos o evento. O que quer que possamos passar em `emit ()` estará disponível para o pai como `$ event`.

Nada mais é alterado no componente todo-input. Os eventos emitidos por `keyup.enter` e` click` ainda chamam o mesmo método, mas o próprio método mudou.
  
O nome do método pode parecer irrelevante agora. Se você quiser, pode mudá-lo para algo mais apropriado, como `submitValue`. Lembre de mudar isso no template também.

```ts
submitValue(newTitle: string) {
  this.submit.emit(newTitle);
}
```
  
```ts
template: `
  <input #inputElementRef
         [value]="title"
         (keyup.enter)="submitValue($event.target.value)">

  <button (click)="submitValue(inputElementRef.value)">
    Save
  </button>
`,
```
  
## Escutando ao Evento
  
Agora, tudo o que precisamos fazer é pegar o evento no componente principal e anexar lógica a ele. Vá para o componente `app-root` e vincule ao evento `submit` no componente `<app-input-button-unit>`:

```html
<app-input-button-unit (submit)="addItem($event)"></app-input-button-unit>
```

Agora tudo oque falta fazer é implementar o método `addItem`, que recebe uma string, cria um objeto com a string como a propriedade `title` e o adiciona a lista:
  
```ts
addItem(title: string): void {    
  this.todoList.push({ title });
}
```

Teste!
  
