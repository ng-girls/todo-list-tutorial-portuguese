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

Check it out in the browser. Now with every key stroke, you can see the title changes and reflects the input value.

### Pressing the Enter key
You can limit the change to only a special key stroke, in our case it's the Enter key. Angular makes it really easy for us. The `keyup` event has properties which are more specific events. So just add the name of the key you'd like to listen to:

```html
<input [value]="title" 
       (keyup.enter)="changeTitle($event.target.value)">
```

Now the title will change only when the user hits the Enter key while typing in the input.

### Tip - explore the $event
You can change the changeTitle method to log the `$event` object in the console. This way you can explore it and see what properties it has. 

Change the method `changeTitle`:
```ts
changeTitle(event): void {
  console.log(event);
  this.title = event.target.value; // the original functionality still works
}
```

Now change the argument you're passing in the template:
```html
<input [value]="title" 
       (keyup.enter)="changeTitle($event)">
```

Try it out!

Don't forget to change back the code before we go on.
