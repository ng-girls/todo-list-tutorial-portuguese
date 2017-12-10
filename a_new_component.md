# Um novo componente

Neste capítulo, escreveremos um novo componente. Isso nos permitirá adicionar um item à lista de tarefas. Será composto pelos elementos HTML `input` e `button`.

Utilizaremos o Angular-CLI para gerar todos os arquivos e boilerplate para nosso app. No seu terminal, execute o seguinte comando:

```cmd
ng g c input -it
```

> Observe que você precisa abrir um novo terminal (janela ou guia) para executar
> o novo comando. Inserindo o comando acima para o shell onde `ng serve` roda
> não terá nenhum efeito.

Como vimos anteriormente, `ng` é o comando para ser usar o Angular-CLI. `g` é um atalho para `generate`. `c` é um atalho para  `component`. `input` é o nome que daremos ao componente. `-it` é um atalho para `--inline-template`.

Então, a versão longa do comando é:

```
ng generate component input --inline-template
```

> Você pode evitar usar `-it` cada vez que você gera um componente configurando modelos inline como padrão no arquivo de configuração `angular-cli.json`.
>
> Não se preocupe com o nome do componente `input`. Ele não irá substituir os elementos HTML `input`. Isso é graças ao prefixo que a Angular-CLI dá aos nossos componentes. O prefixo padrão é `app`, então o seletor de componentes seria `app-input`. Se você criou o projeto indicando o prefixo de sua escolha, ou alterou-o posteriormente no arquivo `angular-cli.json`, este será o prefixo do seletor. Quando criamos o projeto, definimos o prefixo para "todo", então o seletor será `todo-input`.

Vejamos o que a Angular-CLI criou para nós.

Ele criou uma nova pasta chamada `src/app/input`. Existem três arquivos lá:

* `input.component.css` - este é o arquivo em que o estilo específico do componente será colocado.
* `input.component.spec.ts` - este é um arquivo para testar o componente. Não vamos lidar com isso neste tutorial.
* `input.component.ts` - este é o arquivo componente onde vamos definir o modelo e a lógica.

Abra o arquivo `input.component.ts`. Você pode ver que o Angular-CLI gerou um template padrão:

```js
template: `
    <p>
      input Works!
    </p>
  `,
```

Ele também adicionou um seletor de acordo com o nome que do componente, com o prefixo que configuramos:

```js
selector: 'todo-input',
```

Nós podemos usar este componente como está e ver o resultado!

Abra o arquivo root do componente, `app.component.ts` e adicione a tag do todo-input em qualquer lugar do template:

```js
template: `
  <h1>
    {{title}}
  </h1>

  <todo-input></todo-input>
`,
```

Veja as atualizações no browser!

Retorne ao arquivo `input.component.ts` e adicione algum conteúdo. Primeiro, adicione um membro do `title` que usaremos como título do item todo:

```ts
export class InputComponent implements OnInit {
  title: string = '';
  ...
```


Isso não irá interferir com o `title` do componente `todo-root`, uma vez que o conteúdo de cada componente encapsulado dentro dele.

Você pode adicionar uma string inicial ao título, como fizemos no componente `todo-root`.

Em seguida, adicione um elemento de entrada, um botão e um binding ao título, dentro modelo:

```html
<input>
<button>Save</button>
<p>The title is: {{ title }}</p>
```

Veja os resultados!

Este componente não faz muito neste momento. Nos próximos capítulos, aprenderemos sobre a classe de componentes e, em seguida, implementaremos a lógica do componente.
