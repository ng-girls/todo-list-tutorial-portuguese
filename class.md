# Classes


## Definição de classes

A Classe é uma estrutura programática especial. Ela é definida com **membros** que podem ser **propriedades** (variáveis) e **métodos** (funções). As instâncias da uma classe são geralmente criadas chamando-se o operador ```new```: ```let minhaInstancia = new minhaClasse();```. A instância criada é um objeto no qual você poderá chamar os métodos da classe, obter e definir os valores de suas propriedades. É possível criar múltiplas cópias a partir de uma mesma classe.

### No Angular...

O Angular cuida da criação de instâncias das classes que você define - se elas forem reconhecidas como blocos de montar do Angular. Os **decorators** (decoradores) fazem essa conexão com o Angular.

Toda vez que você utiliza um componente em um template, uma nova instância deste é criada. Por exemplo, aqui serão criadas três instâncias da classe inputComponent:

```html
template: `
  <todo-input></todo-input>
  <todo-input></todo-input>
  <todo-input></todo-input>
`
```

Vamos dar uma olhada na classe ```inputComponent```.

### implementa OnInit

Primeiro, você pode ver que algo foi adicionado na declaração da classe:

```ts
export class InputComponent implements OnInit {
  ...
}
```

`OnInit` é uma **interface** - a definição de uma estrura, que não é implementada como uma clase. Ela define quais propriedades e/ou métodos devem existir na classe que a implementa. Neste caso, `OnInit` é uma interface para os componentes Angular que implementam o método `ngOnInit`. Este método é um **método do ciclo de vida do componente**. O Angular irá chamar este método depois que a instância tiver sido criada.

O Angular-CLI adiciona esta declaração para nos lembrar de que é melhor inicializar as coisas no componente através do método `ngOnInit`. Você pode ver que ele também adicionou o método no corpo da classe:

```ts
ngOnInit() {
}
```

Você pode usar esse método sem indicar explicitamente que a classe está implementando a interface OnInit. Mas é útil usar a declaração de implementação. Para ver como, exclua o método `ngOnInit`. A IDE irá lhe dizer que existe um erro - você deve implementar `ngOnInit`. Como ela sabe disso? Por causa do `implementing OnInit`.


### construtor

Outro método que não vimos no componente `todo-root` é o construtor. Este é um método que é chamado pelo JavaScript quando uma instância da classe é criada. O que quer que esteja dentro deste método, será usado para criar a instância. Ele é chamado antes do `ngOnInit`.
> Uma feature importante do Angular que usa o construtor é a injeção de dependência. Abordaremos isso mais tarde, quando começarmos a usar serviços.

### Propriedades

A propriedade `titulo` que adicionamos é utilizada para armazenar um valor, no nosso caso, uma string. Cada instância da classe terá sua própria variável `titulo`, o que significa que você pode alterar o valor do `titulo` em uma instância, mas o valor permanecerá o mesmo para as outras instâncias.

Você pode declarar uma propriedade sem inicializá-la:
```ts
titulo: string;
```

Em seguida, você pode atribuir um valor em um estágio posterior, por exemplo, no construtor ou no método ngOnInit. Ao referenciar um membro da classe de dentro de um método desta classe, você deve prefixá-lo com `this`. Esta é uma propriedade especial que aponta para a instância atual.

Tente definir um valor diferente para o `título` dentro do construtor. Veja o resultado no navegador:

```ts
titulo: string = 'meu título';

constructor() {
  this.titulo = 'Olá mundo';
}
```

Tente alterar o valor de `titulo` dentro do método `ngOnInit`. Qual valor será exibido na tela?

### Métodos

Vamos adicionar um método que altera o valor de `titulo` de acordo com o argumento que passarmos. O método terá um parâmetro do tipo `string`. Adicione-o dentro do corpo da classe (mas não dentro de outro método):

```ts
mudaTitulo(novoTitulo: string): void {
  this.titulo = novoTitulo;
}
```

O método é chamado `mudaTitulo`. Ele não tem uma declaração de retorno, então observamos que ela "retorna void" (vazio). Podemos mudar isso se retornarmos um valor real. Por exemplo:

```ts
mudaTitulo(novoTitulo: string): string {
  this.titulo = novoTitulo;
  return this.titulo;
}
```

Este método não é usado em nenhum lugar. Podemos chamá-lo dentro de outro método ou modelo (o que veremos nos capítulos seguintes). Vamos chamá-lo dentro do construtor.

```ts
constructor() {
  this.mudaTitulo('Eu amo Angular');
}
```

Você pode tentar chamar o método com argumentos diferentes (a string passada dentro dos parênteses) no ngOnInit. Tente chamá-lo antes ou depois de atribuir um valor diretamente ao `titulo`. Tente chamá-lo algumas vezes dentro do mesmo método. Veja o resultado no navegador.


### Dicas de depuração (debug)

Você sempre pode usar o `console.log(algumValor)` dentro de métodos da classe. O valor que você passar como argumento será mostrado no console do navegador. Desta forma, você pode ver a ordem da execução dos métodos e o valor do argumento que você passou (se for uma variável). Por exemplo:

```ts
constructor() {
  console.log('dentro do construtor');
  this.mudaTitulo('Eu amo Angular');
  console.log(this.titulo);
}
```

O console do navegador faz parte de seu Dev Tools. Veja aqui diferentes formas de abrir o console do navegador:[https://webmasters.stackexchange.com/questions/8525/how-do-i-open-the-javascript-console-in-different-browsers](https://webmasters.stackexchange.com/questions/8525/how-do-i-open-the-javascript-console-in-different-browsers)
