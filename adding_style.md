# Adicionando estilo

Com o Angular, podemos dar estilo aos componentes, de uma forma que não afetará o resto da aplicação. É uma boa prática encapsular o estilo relacionado aos componentes desta forma.

Também podemos indicar regras de estilo geral para serem usadas em toda a aplicação. Isso é bom para criar o mesmo look-and-feel para todos os nossos componentes. Por exemplo, podemos decidir qual paleta de cores será usada como o tema do nosso aplicativo. Então, se quisermos mudar as cores ou oferecer diferentes temas, podemos mudá-lo em um só lugar, em vez de em cada componente.

Angular nos dá diferentes métodos de encapsulamento de estilo, mas nos seguiremos com o padrão.

Angular-CLI gerou um estilo geral no `src/style.css`. Cole o código a seguir no arquivo de estilo: 

```css
html, body, div, span,
h1, p, ul, li {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}

body {
  line-height: 1;
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

```
>Como o projeto irá acessar este arquivo? No arquivo de configuração Angular-CLI `.angular-cli.json` em `apps[0].styles` você pode indicar os arquivos para a ferramenta de compilação para levar e adicionar ao projeto. Você pode abrir as ferramentas de desenvolvimento do navegador e ver o estilo dentro do elemento:

```html
<html>
  ...
  <head>
    ...
    <style type="text/css">
    ...Your style is here
    </style>
    ...
  </head>
  ...
</html> 
```


Agora, vamos adicionar um estilo específico para o componente list-manager.

Abra o arquivo `list-manager.component.css` e cole o estilo abaixo:

```css
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

.todo-app:before, .todo-app:after {
  content: '';
  position: absolute;
  z-index: -1;
  height: 4px;
  background: white;
  border: 1px solid #ccc;
  border-radius: 2px;
}

.todo-app:after {
  bottom: -3px;
  left: 0;
  right: 0;
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
}

.todo-app:before {
  bottom: -5px;
  left: 2px;
  right: 2px;
  border-color: #c4c4c4;
  -webkit-box-shadow: 0 1px 2px rgba(0, 0, 0, 0.15);
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.15);
}

.todo-app h1 {
  font-size: 52px;
  line-height: 52px;
  margin-bottom: 30px;
  font-weight: bold;
  text-align: center;
  letter-spacing: -0.8px;
}

.todo-add {
  margin-bottom: 20px;
}
```

Como essa folha de estilo é anexada ao componente `list-manager`?
Olhe o arquivo `list-manager.component.ts`. Uma das propriedades no objeto passado para o decorator `@Component` é `styleUrls`. É uma lista de folhas de estilo a serem usadas pelo Angular, que encapsula o estilo dentro do componente.

Adicione o seguinte estilo a `input.component.css`:
```css
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

Adicione o seguinte estilo a `item.component.css`:
```css
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

.btn-red {
  background: red;
}

.btn-red:hover {
  background: darkred;
}

```
Observe: Não se esqueça de colocar as classes CSS no template de código do seu componente, como o exemplo abaixo:
```ts
 @Component({
    ...
    template: `
          <button class="btn btn-red" (click)="removeItem()">
          `,
```
Você pode mudar o estilo como você quiser - o tamanho dos elementos, as cores - tudo o que você quiser!

Observe: você pode usar arquivos SCSS no projeto, que é uma maneira mais agradável de escrever estilo e possui excelentes recursos que ajudam o desenvolvedor. Os arquivos SCSS são compilados para o css quando o projeto é criado.
