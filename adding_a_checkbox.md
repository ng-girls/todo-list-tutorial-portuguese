# \#19: 🔘 Adicionando um CheckBox

Agora nós somos capazes de interagir com nossa lista removendo itens. Mas, e se quisermos completar itens e ainda poder vê-los em nossa lista, por exemplo, com uma linha no título do item? Aí entra o checkbox!

Nós iremos ver como:

* Adicionar uma checkbox
* Adicionar uma funcionalidade que, quando você clica na checkbox, adiciona uma classe CSS - que adiciona um estilo ~~riscado~~, a ser adicionada aos nossos itens da lista
* Editar a lista para responder ao checkbox
* Adicionar uma nova classe CSS

Agora vamos avançar e adicionar um checkbox em nosso arquivo `todo-item.component.ts`. Coloque o código abaixo antes da tag `{{ item.title }}`:

```html
  <input type="checkbox"/>
```
Agora, para que o checkbox faça alguma coisa, precisamos adicionar um evento de `clique` que chamaremos de `completeItem`. Nós também adicionaremos uma classe css, colocar o elemento envolto e a interpolação juntos para estilo. Vamos fazer isso agora:

```html
  <div>
    <input type="checkbox"
          class="todo-checkbox"
          (click)="completeItem()"/>
    {{ item.title }}
  </div>
```
Quando clicamos no checkbox, o programa irá rodar a função `completeItem`. Vamos falar sobre o que essa função precisa realizar. Nós precisamos adicionar estilos com CSS no título do item, então, quando o checkbox estiver clicado, teremos uma linha riscando ele. Nós também queremos salvar o status do item no local storage. Para alcançar isso, nós iremos emitir um evento de updae com o novo status do item e obter isso no componente pai.

```js
export class TodoItemComponent implements OnInit {
  @Input() item: TodoItem;
  @Output() remove: EventEmitter<TodoItem> = new EventEmitter();
  @Output() update: EventEmitter<any> = new EventEmitter();

  // put this method below ngOnInit
  completeItem() {
    this.update.emit({
      item: this.item,
      changes: {completed: !this.item.completed}
    });
  }
```

Mas espere! Como esse código irá afetar a lista quando estamos apenas tocando o checkbox? Bom, o Angular tem essa maravilhosa diretriz chamada NgClass. Essa diretriz aplica ou remove uma classe CSS baseada num valor booleano (verdadeiro ou falso). Existem diversas maneiras de utilizar essa diretiva ([veja a documentação da diretiva NgClass](https://angular.io/api/common/NgClass)), mas nós iremos focar na utilização abaixo: 

```html
<some-element [ngClass]="{'first': true, 'second': true, 'third': false}">...</some-element>
```

No exemplo acima, a classe 'first' e a 'second' vão ser aplicadas no elemento porque têm valor verdadeiro. Já a 'third' não irá ser aplicada, pois seu valor é falso. É aqui que nosso código anterior começa a fazer sentido. Nossa função `completeItem` irá mudar entre valores verdadeiros e falsos, ditando quando uma classe será aplicada ou removida.

Vamos adicionar o título do item em um `<span>`, então usar NgClass para aplicar o estilo. Dependendo do item atual completado, nós iremos mostrar uma linha de decoração ou não:

```html
<p class="todo-title" [ngClass]="{'todo-complete': item.completed}">
  {{ item.title }}
</p>
```

E, finalmente, adicione o CSS em nosso arquivo `todo-item.component.css`:

```css
  .todo-complete {
    text-decoration: line-through;
  }
```

Próximo passo é falar para o gerenciador de listas do componente pai o que fazer quando o evento de update for emitido. Para fazer isso, nós temos que ligar a ação de update e o método de update que irá acionar a função apropriada no TodoListService. Então aplicamos aqui:

```html
<app-todo-item [item]="todoItem"
               (remove)="removeItem($event)"></app-todo-item>
</div>
```

Próximas modificações:

```html
<app-todo-item [item]="todoItem"
             (remove)="removeItem($event)"
             (update)="updateItem($event.item, $event.changes)"></app-todo-item>
</div>
```

E crie um método adicional para gerenciar o evento de update de item. Muito similar com a função `removeItem`:

```js
updateItem(item, changes) {
  this.todoListService.updateItem(item, changes);
}
```

Voila! Quando você clica no checkbox, o css deve adicionar uma linha no título da lista, e se clicar novamente, o checkbox irá remover a linha.
