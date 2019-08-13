# #14 💅 Adicionando estilo

Com o Angular, podemos estilizar os componentes de uma forma que não afete o resto da nossa aplicação. Dessa forma, é uma boa prática encapsular o estilo relacionado aos componentes.

Também podemos definir regras gerais de estilo para serem usadas em toda a nossa aplicação. Isso é bom para criar a mesma aparência para todos os nossos componentes. Por exemplo, podemos decidir qual paleta de cores será usada como o tema do nosso aplicativo. Então, se quisermos mudar as cores ou oferecer temas diferentes, podemos mudá-lo em um só lugar em vez de cada componente.

O Angular nos oferece diferentes métodos de encapsulamento de estilo, mas nós seguiremos com o padrão.

O Angular-CLI já gerou um estilo geral no `src/style.css`. Cole o código a seguir no arquivo de estilo: 

```css
html, body, div, span,
h1, p, ul, li {
  padding: 0;
  border: 0;
  font: inherit;
  vertical-align: baseline;
}

body {
  background: #f1f1f1;
  font-size: 16px;
  line-height: 22px;
  color: #404040;
  font-family: 'Lucida Grande', Verdana, sans-serif;
}

ol, ul {
  list-style: none;
}

.btn {
  background: lightseagreen;
  color: #fff;
  padding: 3px 10px;
  margin: 0 0 0 3px;
  border: none;
  border-radius: 5px;
  font-size: 12px;
  line-height: 24px;
  cursor: pointer;
  vertical-align: bottom;
}

.btn:hover {
  background: lightslategrey;
}

.btn-red {
  background: red;
}

.btn-red:hover {
  background: darkred;
}

.app-title {
  font-size: 52px;
  line-height: 52px;
  margin-bottom: 30px;
  font-weight: bold;
  text-align: center;
  letter-spacing: -0.8px;
}

```
>Como o projeto irá acessar este arquivo? No arquivo de configuração Angular-CLI `.angular-cli.json` em `projects.todo-list.architect.build.options.styles` você pode definir os arquivos relacionados para que a ferramenta de compilação o reconheça e adicione ao projeto. Você pode abrir as ferramentas de desenvolvimento do navegador e observar o estilo dentro do elemento:

```html
<html>
  ...
  <head>
    ...
    <style type="text/css">
    ...Seu estilo está aqui!
    </style>
    ...
  </head>
  ...
</html> 
```
Nós adicionamos estilos diretamente nos elementos (html, body, div, span, h1, p, ul, li) o que afeta diretamente o nosso aplicativo. Nós também adicionamos estilos utilizando as classes/seletores CSS. Nós precisamos adicionar as classes nos elementos relevantes.

No `app-root`, adicione a classe `app-title` no elemento h1:

-> src/app/app.component.ts
```
template: `
  <h1 class="app-title">
    Bem vindo ao {{ title }}!
  </h1>

  <app-list-manager></app-list-manager>
`,

```

No `input-button`, adicione a classe `btn` no elemento botão:

-> src/app/input-button/input-button.component.ts

```
<button class="btn"
        (click)="submitValue(inputElementRef.value)">
  Save
</button>

```

Agora, vamos adicionar estilos específicos de nossos componentes. 

Adicione o estilo a seguir no `input-button.component.css`: 

```
.todo-input {
  padding: 4px 10px 4px;
  font-size: 16px;
  font-family: 'Lucida Grande', Verdana, sans-serif;
  line-height: 20px;
  border: solid 1px #dddddd;
  border-radius: 5px;
  flex-grow: 1;
}

:host(:not([hidden])) {
  display: flex;
  justify-content: space-between;
  flex-grow: 1;
}

```
Como essa folha de estilo fica atrelada ao componente `input-button`? Dê olha olhada no arquivo `input-button.component.ts`. Uma das propriedades que o objeto passa para o *decorator* `@Component` é o `styleUrls`. Ele é uma lista de folhas de estilo (*stylesheets*) que será utilizado pelo Angular e encapsula o estilo que pertence ao componente.

O seletor `:host` é aplicado no elemento que pertence a esse componente - `<app-input-button>`. Este elemento não faz parte do modelo deste componente. Aparece no modelo do seu pai. É assim que podemos controlar seu estilo a partir do componente.

Nós precisamos adiiconar a classe `todo-input` no elemento `input`: 

-> src/app/input-button-unit/input-button-unit.component.ts

```
<input class="todo-input"
       #inputElementRef
       [value]="title"
       (keyup.enter)="submitValue($event.target.value)">

```
Agora vamos adicionar o estilo específico do componente `list-manager`. Abra o arquivo `list-manager.component.css` e cole o código a seguir: 

-> src/app/list-manager/list-manager.component.css
```
.todo-app {
  position: relative;
  width: 400px;
  padding: 30px 30px 15px;
  background: white;
  border: 1px solid;
  border-color: #dfdcdc #d9d6d6 #ccc;
  border-radius: 2px;
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  margin: 20px auto;
}

.todo-app::before, .todo-app::after {
  content: '';
  position: absolute;
  z-index: -1;
  height: 4px;
  background: white;
  border: 1px solid #ccc;
  border-radius: 2px;
}

.todo-app::after {
  bottom: -3px;
  left: 0;
  right: 0;
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}

.todo-app::before {
  bottom: -5px;
  left: 2px;
  right: 2px;
  border-color: #c4c4c4;
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.15);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.15);
}

```

Nós vamos encapsular o conteúdo desse componente utilizando um elemento `<div>` com toda a classe `todo-app`:

-> src/app/list-manager/list-manager.component.ts

```
template: `
  <div class="todo-app">
    <app-input-button-unit (submit)="addItem($event)"></app-input-button-unit>

    <ul>
      <li *ngFor="let todoItem of todoList">
        <app-todo-item [item]="todoItem"></app-todo-item>
      </li>
    </ul>
  </div>
`,

```
Por fim vamos adicionar o seguinte estilo no `todo-item.component.css`:  

-> src/app/todo-item/todo-item.component.css
```
.todo-item {
  padding: 10px 0;
  border-top: solid 1px #ddd;
  min-height: 30px;
  line-height: 30px;
  display: flex;
  justify-content: space-between;
}

.todo-checkbox {
  flex-shrink: 0;
  margin: auto 1ex auto 0;
}

.todo-title {
  flex-grow: 1;
  padding-left: 11px;
}

```

Encapsule o conteúdo do componente `todo-item` com um elemento `<div>` e a classe `todo-item`


```
<div class="todo-item">
  {{ item.title }}
</div>

```
Nós vamos utilizar as classes `todo-checkbox` e o `todo-title` nos próximos capítulos

Você pode mudar o estilo como você quiser - o tamanho dos elementos, as cores - tudo o que você quiser!

Observe: você pode usar arquivos SCSS no projeto, o que é uma maneira mais agradável de escrever estilo e possui excelentes recursos que ajudam o desenvolvedor. Os arquivos SCSS são compilados para o css quando o projeto é criado.
