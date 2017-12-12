# Adicionando uma CheckBox

Agora nós somos capazes de interagir com nossa lista removendo itens. Mas e se quisermos completar itens e ainda poder vê-los em nossa lista, por exemplo, ter uma marcação no título da nossa lista? Aí entra o Checkbox!

Nós iremos ver como:

* Adicionar uma checkbox
* Adicionar uma funcionalidade que quando você clica na checkbox adiciona uma classe CSS, que adiciona um estilo strike-through é adicionada aos nossos itens da lista
* Editar a lista para responder ao checkbox
* Adicionar uma nova classe CSS

Agora vamos avançar e adicionar uma checkbox em nosso arquivo item.component.ts. Coloque o código abaixo antes da tag `<p>` contendo `{{ todoItem.title}}`:

```html
  <input type="checkbox"/>
```
Agora, para que o checkbox faça alguma coisa, precisamos adicionar um evento de clique que chamaremos de completeItem(). Vamos fazer isso agora:

```html
  <input type="checkbox" (click)="completeItem()"/>
```
Quando clicamos no checkbox o programa irá rodar a função completeItem(). Vamos falar sobre o que essa função precisa fazer. Nós queremos adicionar estilos com CSS em nosso título, assim, quando a checkbox está clicada teremos uma linha riscando ela, e nenhuma linha quando não está clicada. Para fazer isso, nós vamos colocar uma variável que será positiva ou negativa para representar os dois estados da nossa checkbox. Adicione o código abaixo na classe ItemComponent:

```js
isComplete: boolean = false;

completeItem() {
  this.isComplete = !this.isComplete;
}
```

Mas espere! Como esse código irá afetar a lista quando estamos apenas tocando a checkbox? Bom, o Angular2 tem maravilhosas diretrizes chamadas NgClass. Essas diretrizes aplicam ou removem uma classe baseada num valor booleano (verdadeiro ou falso). Existem diversas maneiras de utilizar a NgClass (veja a documentação: https://angular.io/docs/ts/latest/api/common/index/NgClass-directive.html), mas nós iremos focar na utilização abaixo: 

```html
<some-element [ngClass]="{'first': true, 'second': true, 'third': false}">...</some-element>
```

No exemplo acima, a classe 'first' e a 'second' vão aparecer no elemento porque tem valor verdadeiro, já a 'third' não irá ser aplicada pois o valor é falso. E é aqui que nosso código anterior começa a fazer sentido. Nossa função completeItem() irá mudar entre valores verdadeiros e falsos, ditando quando uma classe será aplicada ou removida.

Vamos adicionar nossa NgClass no título da nossa lista agora:

```html
<p class="todo-title" [ngClass]="{'todo-complete': isComplete}">
  {{ todoItem.title }}
</p>
```

E finalmente, adicione o css em nosso arquivo item.component.css

```css
  .todo-complete {
    text-decoration: line-through;
  }
```

Voila! Quando você clica na checkbox, o css adiciona uma linha no título da lista, e se clicar novamente a checkbox irá remover a linha.
