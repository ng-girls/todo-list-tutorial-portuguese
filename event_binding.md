# Eventos

Queremos que nossa aplicação reaja às ações do usuário. Queremos atualizar o título do item de nossa lista toda vez que o usuário trocar o nome, ou adicionar um novo item quando o usuário aperta o botão de Salvar ou a tecla Enter.

Nós ainda não temos uma lista inteira para mostrar, mas no momento iremos usar outra maneira de testar a ação. Nós iremos mudar para a funcionalidade esperada mais tarde.


## A ação
Primeiro, vamos implementar a função `changeTitle`. Você pode trocar o `generateTitle` com esse novo método. Ela irá receber um novo título como argumento:

```ts
changeTitle(newTitle: string): void {
  this.title = newTitle;
}
```

## Ligando os Eventos
Assim como ligar propriedades de um elemento, nós podemos ligar eventos que são emitidos por outros elementos. Novamente, o Angular nos dá uma maneira bem simples de fazer isso. **Você só coloca o nome do evento entre parêntesis e passa o evento no método que deve ser executado quando o evento for emitido**.

Vamos tentar com um exemplo simples, onde o título está mudando quando o usuário clica no botão. Note que existe um parêntesis em volta do `click`. (Nós também trocamos a ligação do input de volta para o valor `title`.)

```html
template: `
  <input [value]="title">
  <button (click)="changeTitle('Button Clicked!')">
    Save
  </button>
  <p>The title is: {{ title }}</p>
`,
```

O evento tem nome de `click` e não `onClick` - em Angular você remove o prefixo `on` dos eventos nos elementos. 

Vá para o navegador e veja o resultado - clique no botão Save.


## Dados do Evento

Passamos uma string estática no método chamada de: `Button Clicked!`. Mas queremos passar o valor que o usuário digitou na lacuna!

No próximo capítulo iremos aprender como usar as propriedades de um elemento em outro elemento no mesmo template. Depois, seremos capazes de completar a implementação do evento click no botão Save. Mas agora nós ligaremos um método em um evento no input: quando o usuário apertar Enter, o método `changeTitle` será chamado.

### Evento 'keyup' 

Quando o usuário digita, eventos do teclado são emitidos. Por exemplo, `keydown` e `keyup`. Nós iremos usar o evento `keyup` \(quando a tecla pressionada é solta) e trocar o título:

```html
<input [value]="title" (keyup)="changeTitle('Button Clicked!')">
```

O elemento começa a ficar grande, então para ficar mais fácil de ver, nós dividiremos em duas linhas:

```html
<input [value]="title" 
       (keyup)="changeTitle('Button Clicked!')">
```
Agora, quando o usuário digitar na lacuna, o título muda para "Button Clicked!". Mas continua uma string estática.

### O objeto do evento

Agora só queremos reagir quando o evento `keyup` ocorre. O Angular permite que nós utilizemos o próprio objeto do evento. Ele é passado pela ligação com o evento como `$event` - assim nós podemos utilizá-lo quando chamamos `changeTitle()`.

O objeto do evento emitido nos eventos `keyup` tem uma referência ao elemento que emite o evento - o elemento de input. A referência é guardada numa propriedade do evento, chamada `target`. Como vimos anteriormente, o elemento de input tem uma propriedade `value` que segura a string que está no input. Nós podemos passar `$event.target.value` para o método:

```html
<input [value]="title" 
       (keyup)="changeTitle($event.target.value)">
```

Teste em seu navegador. Agora, com cada tecla apertada, você consegue ver as mudanças no título e elas refletem o valor do input.

### Apertando a tecla Enter
Você pode limitar a mudança a um clique de tecla, em seu caso é o Enter. Angular deixa tudo bem mais fácil pra nós. O evento `keyup` tem propriedades que são eventos mais específicos. Então, adicione o nome da tecla que seu evento escutará:

```html
<input [value]="title" 
       (keyup.enter)="changeTitle($event.target.value)">
```

Agora o título irá mudar apenas quando o usuário apertar a tecla Enter enquanto digita no input.

### Dica - explore o $event
Você pode mudar o método changeTitle para registrar o objeto `$event` no console. Dessa forma você pode explorar e ver quais propriedades ele tem.

Mude o método para `changeTitle`:
```ts
changeTitle(event): void {
  console.log(event);
  this.title = event.target.value; // the original functionality still works
}
```

Agora, mude o argumento que você está passando no modelo:

```html
<input [value]="title" 
       (keyup.enter)="changeTitle($event)">
```

Teste!

Não esqueça de voltar para o código anterior à dica antes de continuar o tutorial.

**Traduzido por Mariana Abad**
