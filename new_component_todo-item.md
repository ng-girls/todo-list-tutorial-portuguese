# \#10: ➕ Novo componente todo-item

Vamos criar um novo componente que mostre cada todo-item presente na lista. Será um componente simples no começo, mas irá crescer posteriormente. O importante é que **ele receberá o todo-item como uma entrada do componente pai**. Deste modo poderá ser um componente reutilizável, e não dependerá diretamente dos dados e estados da aplicação.

Crie um novo componente chamado `todo-item`: 

```bash
ng g c todo-item
```

Você pode ver uma nova pasta criada - `src/app/todo-item` com os arquivos do componente.

Use o novo componente no template do `app-root` - dentro do elemento `<li>`:

```html
<ul>
  <li *ngFor="let todoItem of todoList">
    <app-todo-item></app-todo-item>
  </li>
</ul>
```

Confira o resultado no navegador. O que você vê? Por que?

## @Input\(\)

Nós queremos exibir o título de cada item dentro do componente `todo-item`. Precisamos passar o título atual do item no loop (ou o item inteiro) para o o componente `todo-item`. 

Novamente, Angular faz com que seja muito fácil para nós, fornecendo-nos o decorator `Input`.

Dentro da classe recém criada `TodoItemComponent` em `todo-item.component.ts` adicione a linha:

{% code-tabs %}
{% code-tabs-item title="src/app/todo-item/todo-item.component.ts" %}
```ts
@Input() item;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Ele diz ao componente para esperar uma entrada e a atribuir ao membro da classe `item`. Certifique-se de que `Input` está adicionado na declaração de importação na primeira linha do arquivo. Agora podemos usá-lo  dentro do `todo-item` template e extrair o título do item com a interpolação : `{{ item.title }}`

O componente deverá ser apresentado como:

{% code-tabs %}
{% code-tabs-item title="src/app/todo-item/todo-item.component.ts" %}
```typescript
import { Component, Input, OnInit } from '@angular/core';

@Component({
  selector: 'app-todo-item',
  template: `
    {{ item.title }}
  `,
  styleUrls: ['./todo-item.component.css']
})
export class TodoItemComponent implements OnInit {
  @Input() item;

  constructor() { }

  ngOnInit() {
  }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Agora nós precisamos passar um item do qual utilizamos o componente. Volte para o componente `app-root` e passe o título do item para o `todo-item`.

```html
<ul>
  <li *ngFor="let todoItem of todoList">
    <app-todo-item [item]="todoItem"></app-todo-item>
  </li>
</ul>
```

O `item` entre colchetes é o mesmo declarado como o `@Input` do componente.

Usamos a vinculação de propriedades em um elemento que nós mesmas criamos! E agora podemos realmente ver e entender que a vinculação de propriedades se vincula a uma propriedade real do componente. Em breve, veremos como essa lista pode ser dinâmica.
