# 4# ✏ Um novo componente

Neste capítulo nós escreveremos um componente totalmente novo. Isso permitirá que nós adicionemos um item a nossa lista de tarefas, que será composto pelos elementos HTML `input` e `button`. Nós vamos chamá-lo de **Input-Button-Unit**

Utilizaremos o Angular-CLI para gerar todos os arquivos que precisamos para nosso app. O Angular CLI utiliza comandos em um terminal. Isso não signfica que teremos de parar o processo `ng serve`. Ao vez disso, podemos abrir um novo terminal (janela ou aba) e executar os comandos adicionais. Dessa forma, o que for modificado será atualizado imediatamente no navegador.

Abra um **novo** terminal e execute o seguinte comando:

```text
ng g c input-button-unit
```

{% hint style="info" %}
**StackBlitz Instructions** ![](https://github.com/ng-girls/todo-list-tutorial/tree/2e565be398494ef864f39582b7dac2c0f55a8fd1/a-new-component/.gitbook/assets/stackblitz-hint.svg)

Nós iremos usar o Angular Generator para criar um componente. Siga as instruções da página [StackBlitz instructions](stackblitz.md) e retorne para continuar o tutorial.


Como vimos anteriormente, `ng`é um comando do Angular-CLI. `g` é a forma abreviada de `generate` que significa "gerar"; `c` é a forma abreviada para `component` que representa a palavra "componente". `input-button-unit` é o nome que demos para o nosso component.

A versão longa do comando seria essa (Não execute!):

```text
ng generate component input-button-unit
```

Agora vamos dar uma olhada no que o Angular-CLI criou para nós. 

Foi criado uma nova pasta chamada `src/app/input-button-unit`. É possível identificar três documentos ali (ou 4, se você não estiver usando inline-template):

`input-button-unit.component.css` - onde fica o estilo específico do componente.
`input-button-unit.component.spec.ts` - é um documento de testes. Não falaremos dele nesse tutorial
`input-button-unit.component.ts` - onde colocaremos a lógica do nosso componente.
`input-button-unit.component.html` - onde fica o seu template HTML se você não estiver utilizando inline-template.

Abra o documento `input-button-unit.component.ts`. Você pode notar que o Angular-CLI já gerou toda a configuração inicial desse componente para nós, inclusive o seu seletor, que é o nome que nós demos precedido pelo prefixo `app`, e um template padrão.

{% code title="src/app/input-button-unit/input-button-unit.component.ts" %}
```typescript
@Component({
  selector: 'app-input-button-unit',
  templateUrl: './input-button-unit.component.html',
  styleUrls: ['./input-button-unit.component.css']
})
```
{% endcode %}

> Note que o prefixo `app` será adicionado no seletor de todos os componentes que você criar. Isso é para evitar que haja conflito entre o nome do componente criado e os elementos HTML. Dessa forma, se você criar um componente `input` ele não entrará em conflito com a tag HTML `<input>`, já que o seletor do seu componente será `app-input`.

> `app` é um prefixo padrão, o que é ótimo para sua aplicação principal. Entretanto, se você está escrevendo uma biblioteca de componentes para ser utilizado em outros projetos, você pode utilizar um prefixo diferente. Por exemplo, a biblioteca do [Angular Material](https://material.angular.io/) usa o prefixo `mat` para seus componentes. Você pode criar um projeto com o prefixo da sua preferência usando o comando `--prefix`, ou modificando posteriormente no documento `angular.json`

Nós podemos usar este componente como está e ver o resultado!

Abra o arquivo root do componente, `app.component.ts` e adicione a tag do `app-input-button-unit` dentro do template \(lembre-se que nós refatoramos o componente root para utilizar o inline template):

{% code title="src/app/app.component.ts" %}
```markup
template: `
  <h1>
    Welcome to {{ title }}!
  </h1>

  <app-input-button-unit></app-input-button-unit>
`,
```
{% endcode %}

Veja as atualizações no browser!

Vamos adicionar um novo conteúdo no seu novo componente. Primeiro, adicione um membro do `title` que usaremos como título do item todo:

{% code title="src/app/input-button-unit/input-button-unit.component.ts" %}
```typescript
export class InputButtonUnitComponent implements OnInit {
  title = 'Hello World';
```
{% endcode %}

Isso não irá interferir com o `title` do componente `app-root`, uma vez que o conteúdo de cada componente encapsulado dentro dele.

Em seguida, adicione um elemento de entrada, um binding ao título, dentro modelo:

{% code title="src/app/input-button-unit/input-button-unit.component.ts" %}
```markup
template: `
  <p>
    input-button-unit works!
    The title is: {{ title }}
  </p>
`,
```
{% endcode %}

Veja os resultados!

Este componente não faz muito neste momento. Nos próximos capítulos, aprenderemos sobre a classe de componentes e, em seguida, implementaremos a lógica do componente.

{% hint style="success" %}
[See the results on StackBlitz](https://stackblitz.com/github/ng-girls/todo-list-tutorial/tree/master/examples/04-a-new-component%20)
{% endhint %}