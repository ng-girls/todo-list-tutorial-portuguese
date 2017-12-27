# Element ref

No último capítulo, nós terminamos com o componente input que pode refletir e mudar o valor do título do nosso item todo.
`input.component.ts` deve estar igual a:

```javascript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'todo-input',
  template: `                           
    <input [value]="title"              
           (keyup.enter)="changeTitle($event.target.value)">
    <button (click)="changeTitle('Button Clicked!')">
      Save
    </button>
    <p>The title is: {{ title }}</p>
  `,  
  styleUrls: ['./input.component.css']  
})    
export class InputComponent implements OnInit {
  title: string = '';           

  constructor() { }                     

  ngOnInit() {
  }

  changeTitle(newTitle: string): void {
    this.title = newTitle;              
  }
}
```

Agora, queremos pegar o valor do input (o que o usuário escreveu) e mudar o título quando for pressionado o botão de salvar.

Nós já sabemos como criar um botão e reagir para clicar nele. Agora nós precisamos passar para o método alguma informação de algum elemente diferente. Agora precisamos passar para o método alguns dados de um elemento diferente. Queremos usar o valor da entrada dentro do elemento do botão.

O Angular nos ajuda a fazer exatamente isso. **Podemos obter uma referência ao elemento que queremos em uma variável com o nome que escolhemos, como por exemplo** `inputElement`, usando uma sintaxe simple - uma hash. ** Adicione um `#inputElement` no `input` e use-o no evento click do botão:

```html
<input [value]="title"              
       (keyup.enter)="changeTitle($event.target.value)"
       #inputElement>

<button (click)="changeTitle(inputElement.value)">
  Save
</button>
```

Agora, podemos usar o valor que o usuário inseriu no elemento de entrada no método chamado ao clicar no botão Salvar.

O que é o `#` que vemos ?

O Angular nos deixa definir uma nova variável local chamada `inputElement` \(ou qualquer nome que você desejar\) que contém uma referência ao elemento em que a definimos e a use de qualquer maneira que desejamos. Em nosso caso, para acessar a propriedade de valor da entrada.

Ao invés de caçar os elementos via DOM query \(o que é uma má prática como já discutimos\), agora podemos colocar referências de elementos no template e acessar cada elemento que queremos declarativamente.

Em seguida, vamos construir a lista de itens todo.

### Dica - explore a referência do elemento

Assim como fizemos no capítulo anterior, quando registramos $event, você pode fazer o mesmo com `#ResourcesinputElement`. Altere o método `changeTitle` para que ele receba toda a referência do elemento e registre-o no console.

```html
<input [value]="title"              
       (keyup.enter)="changeTitle(inputElement)"
       #inputElement>

<button (click)="changeTitle(inputElement)">
  Save
</button>
```
```ts
changeTitle(inputElementReference): void {
  console.log(inputElementReference);
  this.title = inputElementReference.value;              
}

```

## Recursos

[Angular Template Reference Variables](https://angular.io/docs/ts/latest/guide/template-syntax.html#!#ref-vars)

