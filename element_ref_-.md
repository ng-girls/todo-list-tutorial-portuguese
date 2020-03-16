
# \#8: 📎 Element ref - \#

Ao final do último capítulo, nosso component input estava apto para exibir e mudar o título do nosso item. O arquivo `input.component.ts` deve estar assim:

{% code title="src/app/input-button-unit/input-button-unit.component.ts" %}
```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-input-button-unit',
  template: `
    <p>
      input-button-unit works!
      The title is: {{ title }}
    </p>

    <input [value]="title"
           (keyup.enter)="changeTitle($event.target.value)">

    <button (click)="changeTitle('Button Clicked!')">
      Save
    </button>
  `,  
  styleUrls: ['./input-button-unit.component.css']  
})    
export class InputButtonUnitComponent implements OnInit {
  title = 'Hello World';

  constructor() { }                     

  ngOnInit() {
  }

  changeTitle(newTitle: string) {
    this.title = newTitle;
  }
}
```
{% endcode %}

Primeiro, devemos remover uma parte do template que não precisamos. Remova estas linhas:

{% code title="remove this from src/app/input-button-unit/input-button-unit.component.ts" %}
```markup
<p>
  input-button-unit works!
  The title is: {{ title }}
</p>
```
{% endcode %}

Agora queremos pegar o valor do input \(que o usuário digitou\) e mudar o título quando o botão `Save` for clicado.

Nos já sabemos como criar um botão e capturar o evento de clique. Agora precisamos passar para o método valores de um elemento diferente. Queremos usar o valor do `input` dentro do elemento `button`.

O Angular nos ajuda a fazer exatamente isso. **Nós conseguimos guardar a referência de um elemento que queremos em uma variável com o nome que escolhermos,** por exemplo `inputElementRef`, **usando uma sintaxe simples - um hash.** Adicione `#inputElementRef` no elemento de `input` e use no evento `click` do botão:

{% code title="src/app/input-button-unit/input-button-unit.component.ts" %}
```markup
template: `
  <input #inputElementRef
         [value]="title"
         (keyup.enter)="changeTitle($event.target.value)">

  <button (click)="changeTitle(inputElementRef.value)">
    Save
  </button>
`,
```
{% endcode %}

Agora podemos usar o valor que o usuário inseriu no elemento de `input` dentro do método chamado pelo clique do botão `Save`!


## O que é a `#` que usamos?

O Angular nos permite definir uma variável local chamada `inputElementRef` \(ou um nome de sua preferência\), que contém a referência do elemento definido, e utilizá-la da forma que desejarmos. No nosso caso, nós usamos para acessar a propriedade `value` do `input`.

Ao invés de buscar os elementos via DOM query \(que é uma prática ruim, como já discutimos anteriormente\), agora podemos inserir referências via template e acessar o elemento que queremos declarativamente.

Em seguida, vamos criar a lista.

{% hint style="success" %}
[Veja os resultados através do StackBlitz](https://stackblitz.com/github/ng-girls/todo-list-tutorial/tree/master/examples/08-element-ref)
{% endhint %}