# \#12: 📌Adicionando itens

Queremos adicionar itens à nossa lista. Com Angular podemos fazer isso facilmente e ver o item adicionado imediatamente. Vamos fazer isso dentro do `input-button-unit` que criamos antes. Vamos mudá-lo assim, ao pressionar a tecla Enter ou clicar no botão enviar, o valor da caixa de entrada se tornará o título do novo item e o novo item será adicionado à lista.

Mas não queremos que o componente `input-button-unit` seja responsável por adicionar um novo item para a lista. Queremos que ele tenha uma responsabilidade mínima, e **delegue a ação em seu componente pai**. Uma das vantagens desta abordagem é que este componente será reutilizável e pode ser anexado a uma ação diferente em diferentes situações.

Por exemplo, em nosso caso, seremos capazes de usar o `input-button-unit` dentro do componente `todo-item`. Então, teremos uma caixa de entrada para cada item e seremos capazes de editar o título do item. Neste caso, pressionando a tecla Enter ou o botão Salvar terá um efeito diferente.

Então, o que realmente queremos fazer é **emitir um evento** do componente `input-button-unit` sempre que o título for alterado. Com o Angular, podemos facilmente definir e emitir eventos de nossos componentes!

## @Output()

Dentro da classe `InputButtonUnitComponent` adicione a linha de código a seguir, que define uma saída para o componente.

{% code title="src/app/input-button-unit/input-button-unit.component.ts" %}
```typescript
@Output() submit: EventEmitter<string> = new EventEmitter();
```
{% endcode %}

A propriedade de saída será chamada de `submit`. Ela será do tipo `EventEmitter` que possui o método `emit`. `EventEmitter` é um tipo genérico (Generic Type) - nós passamos outro tipo que poderá ser utilizado internamente, nesse caso será uma `string`. É o tipo do objeto que será emitido pelo método `emit`.
  
Certifique-se de que `Output` e o `EventEmitter` foram adicionados à declaração de importação na primeira linha do arquivo:

{% code title="src/app/input-button-unit.component.ts" %}
```typescript
import { Component, OnInit, Output, EventEmitter} from '@angular/core';
```
{% endcode %}

Agora, sempre que chamamos `this.submit.emit()` um evento será emitido para o componente pai. Vamos chamá-lo no método `changeTitle`:

{% code title="src/app/input-button-unit/input-button-unit.component.ts" %}
```typescript
changeTitle(newTitle: string) {
  this.submit.emit(newTitle);
}
```
{% endcode %}

Delegamos tudo ao componente pai - mesmo que altere o título do item, se necessário.  
  
Passamos `newTitle` quando emitimos o evento. O que quer que possamos passar em `emit ()` estará disponível para o pai como `$event`. Os eventos emitidos por `keyup.enter` e` click` ainda chamam o mesmo método, mas o próprio método mudou.

O nome do método não combina mais com a sua ação. Vamos mudar para um nome mais apropriado: `submitValue`. Você pode usar as ferramentas da IDE para renomear o nome do método - lembre-se de mudar isso no template também.

{% code title="src/app/input-button-unit/input-button-unit.component.ts" %}
```typescript
submitValue(newTitle: string) {
  this.submit.emit(newTitle);
}
```
{% endcode %}
  
{% code title="src/app/input-button-unit/input-button-unit.component.ts" %}
```markup
template: `
  <input #inputElementRef
         [value]="title"
         (keyup.enter)="submitValue($event.target.value)">

  <button (click)="submitValue(inputElementRef.value)">
    Save
  </button>
`,
```
{% endcode %}
  
## Escutando ao Evento
  
Agora, tudo o que precisamos fazer é pegar o evento no componente pai e anexar lógica a ele. Vá para o componente `app-root` e vincule ao evento `submit` no componente `<app-input-button-unit>`:

{% code title="src/app/app.component.ts" %}
```markup
<app-input-button-unit (submit)="addItem($event)"></app-input-button-unit>
```
{% endcode %}

Agora tudo oque falta fazer é implementar o método `addItem`, que recebe uma string, cria um objeto com a string como a propriedade `title` e o adiciona a lista:
  
{% code title="src/app/app.component.ts" %}
```typescript
addItem(title: string) {    
  this.todoList.push({ title });
}
```
{% endcode %}

Teste. Informe um novo item ao ToDo no campo e confirme!  
  
**Nota:** Estamos utilizando a notação abreviada (**ES6 Object Property Value Shorthand**) para criar o objeto do item da lista. Quando usamos uma variável que possui o mesmo nome da propriedade do objeto, podemos utilizar essa notação abreviada. No nosso caso `{title}` é o equivalente a `{ title: title }`. Se a variável tivesse um nome diferente, não poderíamos utilizar a notação. Por exemplo:  
  
{% code title="code for example" %}
```typescript
addItem(value: string) {    
  this.todoList.push({ title: value });
}
```
{% endcode %}

{% hint style="success" %}
[See the results on StackBlitz](https://stackblitz.com/github/ng-girls/todo-list-tutorial/tree/master/examples/12-add-items)
{% endhint %}
