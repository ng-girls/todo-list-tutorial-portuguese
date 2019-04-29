
# \#8: 📎 Element ref - \#

No último capítulo, nós terminamos o component input mudando o título da nossa lista de todo. O arquivo `input.component.ts` deve ficar assim:

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}
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
{% endcode-tabs-item %}
{% endcode-tabs %}

Primeiro, devemos remover um pouco do template que não precisamos. Remova estas linhas:

{% code-tabs %}
{% code-tabs-item title="remove this from src/app/input-button-unit/input-button-unit.component.ts" %}
```markup
<p>
  input-button-unit works!
  The title is: {{ title }}
</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Agora queremos pegar o valor do input \(que o usuário digitou\) e mudar o título quando o botão `Save` for clicado.

Nos já sabemos como criar um botão e capturar o evento de clique. Agora precisamos passar para o método valores de um elemento diferente. Queremos usar o valor do `input` de dentro do elemento `button`.

O Angular nos ajuda a fazer exatamente isso. **Nós conseguimos guardar a referência de um elemento que queremos em uma variável com o nome que escolhermos,** por exemplo `inputElementRef`, **usando uma sintaxe simples como a hash.** Adicione `#inputElementRef` no elemento de input, e use no evento de `click` do botão:

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}
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
{% endcode-tabs-item %}
{% endcode-tabs %}

Agora podemos usar o valor que o usuário inseriu no elemento de `input` no método chamado pelo clique do botão `Save`!


### O que é a `#` que usamos?

O Angular permite definir uma variável local chamada `inputElementRef` \(ou um nome de sua preferência\) que contém a referência do elemento definido, e a use da melhor forma que desejarmos. No nosso caso, nós usamos para acessar a propriedade `value` do `input`.

Ao invés de buscar os elementos via DOM query \(o que é uma pratica ruim, como já discutimos anteriormente\), agora podemos inserir referências via template e acessar o elemento que queremos declarativamente.

Em seguida, vamos criar a lista de todo.

## Explore as referências do elemento


Assim como fizemos no capítulo anterior, quando registramos o $event, você pode fazer o mesmo com `#inputElementRef`.

![lab-icon](.gitbook/assets/lab%20%283%29.jpg) Altere o método `changeTitle` para que ele receba toda a referência do elemento e registre-o no console.

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}
```markup
<input #inputElementRef
       [value]="title"              
       (keyup.enter)="changeTitle(inputElementRef)">

<button (click)="changeTitle(inputElementRef)">
  Save
</button>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```typescript
changeTitle(inputElementReference) {
  console.log(inputElementReference);
  this.title = inputElementReference.value;
}
```
Não se esqueça de colocar o código de volta do jeito que estava depois de terminar de experimentar! É melhor passar para um método exatamente o valor que ele precisa, em vez do objeto inteiro.

## Referências

[Angular Template Reference Variables](https://angular.io/guide/template-syntax#template-reference-variables--var-)
