# #5: 💼 Classes

A Classe é uma estrutura programática especial. Ela é definida com **membros** que podem ser **propriedades** (variáveis) e **métodos** (funções). As instâncias da uma classe são geralmente criadas chamando-se o operador ```new```: ```let myInstance = new myClass();```. A instância criada é um objeto no qual você poderá chamar os métodos da classe, obter e definir os valores de suas propriedades. É possível criar múltiplas cópias a partir de uma mesma classe.

### No Angular...

O Angular cuida da criação de instâncias das classes que você define - se elas forem reconhecidas como blocos de construção do Angular. Os **decorators** (decoradores) fazem essa conexão com o Angular.

Toda vez que você utiliza um componente em um template, uma nova instância deste é criada. Por exemplo, aqui serão criadas três instâncias da classe inputComponent:

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```markup
// exemplo

template: `
  <app-input-button-unit></app-input-button-unit>
  <app-input-button-unit></app-input-button-unit>
  <app-input-button-unit></app-input-button-unit>
`,
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Vamos dar uma olhada na classe ```InputButtonUnitComponent```.

### implementa OnInit

Primeiro, você pode ver que algo foi adicionado na declaração da classe:

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}

``` ypescript
export class InputButtonUnitComponent implements OnInit {
  ...
}
```

{% endcode-tabs-item %}
{% endcode-tabs %}

`OnInit` é uma **interface** - a definição de uma estrutura, que não é implementada como uma classe. Ela define quais propriedades e/ou métodos devem existir na classe que a implementa. Neste caso, `OnInit` é uma interface para os componentes Angular que implementam o método `ngOnInit`. Este método é um **método do ciclo de vida do componente**. O Angular irá chamar este método depois que a instância tiver sido criada.

O Angular-CLI adiciona esta declaração para nos lembrar de que é melhor inicializar as coisas no componente através do método `ngOnInit`. Você pode ver que ele também adicionou o método no corpo da classe:

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}

```typescript
ngOnInit() {
}
```

{% endcode-tabs-item %}
{% endcode-tabs %}

Você pode usar esse método sem indicar explicitamente que a classe está implementando a interface OnInit. Mas é útil usar a declaração de implementação. Para ver como, exclua o método `ngOnInit`. A IDE irá lhe dizer que existe um erro - você deve implementar `ngOnInit`. Como ela sabe disso? Por causa do `implementing OnInit`.

### construtor

Outro método que não vimos no componente `app-root` é o construtor. Este é um método que é chamado pelo JavaScript quando uma instância da classe é criada. O que quer que esteja dentro deste método, será usado para criar a instância. Ele é chamado antes do `ngOnInit`.
> Uma feature importante do Angular que usa o construtor é a injeção de dependência. Abordaremos isso mais tarde, quando começarmos a usar serviços.

### Propriedades

A propriedade `title` que adicionamos é utilizada para armazenar um valor, no nosso caso, uma string. Cada instância da classe terá sua própria variável `title`, o que significa que você pode alterar o valor do `title` em uma instância, mas o valor permanecerá o mesmo para as outras instâncias.

No TypeScript, nós devemos declarar os membros de uma classe no corpo dela, fora de qualquer método ou passar eles no construtor - como veremos quando usarmos serviços.

Você pode declarar uma propriedade sem inicializá-la:

```typescript
title: string;
```

Em seguida, você pode atribuir um valor em um estágio posterior, por exemplo, no construtor ou no método ngOnInit. Aqui nós declaramos explicitamente que `title` é do tipo `string`. \(O tipo é inferido pelo TypeScript quando nós atribuímos um valor imediatamente após a declaração, assim não há necessidade em declarar esse tipo no caso.\)

Ao referenciar um membro da classe de dentro de um método desta classe, você deve prefixá-lo com `this`. Esta é uma propriedade especial que aponta para a instância atual.

Tente definir um valor diferente para o `title` dentro do construtor. Veja o resultado no navegador:

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}

```typescript
title = 'Hello World';

constructor() { 
  this.title = 'I Love Angular';
}
```

{% endcode-tabs-item %}
{% endcode-tabs %}

Tente alterar o valor de `title` dentro do método `ngOnInit`. Qual valor será exibido na tela?


{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}

```typescript
title: string = 'Hello World';

constructor() { 
  this.title = 'I Love Angular';
}

ngOnInit() { 
  this.title = 'Angular CLI Rules!';
}
```

{% endcode-tabs-item %}
{% endcode-tabs %}

### Métodos

Vamos adicionar um método que altera o valor de `title` de acordo com o argumento que passarmos. O método terá um parâmetro do tipo `string`. Adicione-o ***dentro do corpo da classe*** /(mas não dentro de outro método/):


{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}

```typescript
changeTitle(newTitle: string) {
  this.title = newTitle;
}
```

{% endcode-tabs-item %}
{% endcode-tabs %}

**Nota:** Funções e Métodos podem retornar um valor que podem ser usados quando um método é chamado. Por exemplo:

{% code-tabs %}
{% code-tabs-item title="code for example" %}

```typescript
function multiply (x: number, y: number) {
  return x * y;
}

let z = multiply(4, 5);
console.log(z);
```

{% endcode-tabs-item %}
{% endcode-ta

O método `changeTitle` não é usado em nenhum lugar. Podemos chamá-lo dentro de outro método ou modelo \(o que veremos nos capítulos seguintes\). Vamos chamá-lo dentro do construtor.

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}

```typescript
constructor() { 
  this.changeTitle('My First Angular App');
}
```

{% endcode-tabs-item %}
{% endcode-tabs %}

**Playground**: Você pode tentar chamar o método com diferentes argumentos\(a string pode ser passada entre colchetes\) no `ngOnInit`. Tente chamar antes ou depois de atribuir um valor diretamente no título. Tente chamar algumas vezes do mesmo método. Veja os resultados no navegador

### Dicas de depuração (debug)

Você sempre pode usar o `console.log(algumValor)` dentro de métodos da classe. O valor que você passar como argumento será mostrado no console do navegador. Desta forma, você pode ver a ordem da execução dos métodos e o valor do argumento que você passou (se for uma variável). Por exemplo:

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}

```typescript
constructor() { 
  console.log('in constructor');
  this.changeTitle('My First Angular App');
  console.log(this.title);
}

changeTitle(newTitle: string) {
  console.log(newTitle);
  this.title = newTitle;
}
```

{% endcode-tabs-item %}
{% endcode-tabs %}

O console do navegador faz parte de seu Dev Tools. Veja aqui diferentes formas de abrir o console do navegador:[https://webmasters.stackexchange.com/questions/8525/how-do-i-open-the-javascript-console-in-different-browsers](https://webmasters.stackexchange.com/questions/8525/how-do-i-open-the-javascript-console-in-different-browsers)
