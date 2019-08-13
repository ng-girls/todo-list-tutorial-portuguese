# 4# ✏ Um novo componente

Neste capítulo nós escreveremos um componente totalmente novo. Isso permitirá que nós adicionemos um item a nossa lista de tarefas, que será composto pelos elementos HTML `input` e `button`. Nós vamos chamá-lo de **input-button**

Utilizaremos o Angular-CLI para gerar todos os arquivos que precisamos para nosso app. Nós podemos abrir um novo terminal (janela ou aba) ao invés de parar o processo do `ng serve`. Dessa forma, o que for modificado será atualizado imediatamente no navegador.

Abra um **novo** terminal e execute o seguinte comando:

```cmd
ng g c input-button
```

Como vimos anteriormente, `ng`é um comando do Angular-CLI. `g` significa "gerar"; `c` representa a palavra "componente". input-button é o nome que demos para o nosso component.

A versão longa do comando seria essa (Não execute!):
```cmd
ng generate component input-button
```
Agora vamos dar uma olhada no que o Angular-CLI criou para nós. É possível identificar três documentos ali (ou 4, se você não estiver usando inline-template):

`input-button.component.css` - onde fica o estilo específico do componente.
`input-button.component.spec.ts` - é um documento de testes. Não falaremos dele nesse tutorial
`input-button.component.ts` - onde colocaremos a lógica do nosso componente.
`input-button.component.html` - onde fica o seu template HTML se você não estiver utilizando inline-template.

Abra o documento `input-button.component.ts`. Você pode notar que o Angular-CLI já gerou toda a configuração inicial desse componente para nós, inclusive o seu seletor e um template padrão. 

Aqui utilizaremos o inline-template para visualizar melhor o nosso componente

-> src/app/input-button-unit/input-button-unit.component.ts
```
@Component({
  selector: 'app-input-button',
  template: `
    <p>
      input-button works!
    </p>
  `,
  styleUrls: ['./input-button.component.css']
})
```

> Note que o prefixo `app` será adicionado no seletor de todos os componentes que você gerar. Isso é para evitar que haja conflito entre o nome do componente criado e os elementos HTML. Dessa forma, se você criar um componente `input` ele não entrará em conflito com a tag HTML `<input>`, já que o seletor do seu componente será `app-input`.

> `app` é um prefixo padrão, o que é ótimo para sua aplicação principal. Entretanto, se você está escrevendo uma biblioteca de componentes para ser utilizado em outros projetos, você pode utilizar um prefixo diferente. Por exemplo, a biblioteca do Angular Material usa o prefixo `mat` para seus componentes. Você pode criar um projeto com o prefixo da sua preferência usando o comando `--prefix`, ou modificando posteriormente no documento `angular.json`

Nós podemos usar este componente como está e ver o resultado!

Abra o arquivo root do componente, `app.component.ts` e adicione a tag do `app-input-button` em qualquer lugar do template:

```
template: `
  <h1>
    Bem vindo ao {{ title }}!
  </h1>

  <app-input-button></app-input-button>
`,
```

Veja as atualizações no browser!

Vamos adicionar um novo conteúdo no seu novo componente! Primeiro, retorne ao arquivo `input.component.ts` e adicione um membro do `title` que usaremos como título do item todo:

```ts
export class InputButtonComponent implements OnInit {
  title: 'Hello World';
  ...
```

Isso não irá interferir com o `title` do componente `app-root`, uma vez que o conteúdo de cada componente encapsulado dentro dele.

Em seguida, adicione um elemento de entrada, um botão e um binding ao título, dentro modelo:

```ts
template: `
  <p>
    input-button works!
    O título é {{ title }}
  </p>
`,
```

Veja os resultados!

Este componente não faz muito neste momento. Nos próximos capítulos, aprenderemos sobre a classe de componentes e, em seguida, implementaremos a lógica do componente.
