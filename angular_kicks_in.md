# \#2: 🅰 Angular entra em ação

Vamos olhar para o projeto e como Angular entra em cena. Se você ainda não fez, abra a pasta todo-list no seu IDE, assim podemos inspecionar os arquivos. Todos os arquivos relevantes a partir desta fase existem dentro da pasta `src`.

Leia mais sobre os arquivos gerados pelo Angular-CLI em [Apêndice 1: Gerando um novo projeto](./generating_a_new_project.html).

Se você está realmente ansioso para começar a codificar, você pode pular este capítulo e voltar mais tarde para entender a estrutura do projeto.

Abra o arquivo `index.html`. O conteúdo que é processado na janela do navegador é tudo o que você vê dentro do elemento `<body>`. Tudo o que você pode ver agora é outro elemento não-HTML: `<app-root></app-root>`. Este elemento é realmente um Componente Angular, definido no arquivo `app/app.component.ts` com a classe chamada **AppComponent**. (Vamos dar uma olhada nisso no próximo capítulo).

> O Angular pode ser definido de muitas maneiras. Uma delas é o código JavaScript que é executado quando o aplicativo é apresentado no navegador. Todo o código que você vai escrever - componentes, módulos, serviços, etc. será reconhecido pelo Angular. O Angular realizará ações de acordo. Por exemplo, os componentes que você irá escrever e usar serão compilados para funções de JavaScript. Essas funções inserem o conteúdo do componente no DOM - o Document Object Model que o navegador usa para mostrar a aplicação. É assim que você verá o componente que você criou na tela.

Então `<app-root>` não é um elemento HTML, é um Componente do Angular. Quando a aplicação está pronta, o conteúdo do componente é inserido na tag `<app-root>`, e verás-lo no navegador:

![Angular Installation Result](/assets/installation-result.png)

Angular precisa que definamos o que queremos que ele compile. Para isso, definimos módulos do Angular, ou **NgModules**, que são como pacotes de coisas relacionadas. Esses pacotes podem incluir componentes, serviços, diretivas, pipes e outros NgModules. Nós já temos um ngModule na raiz definido para nós no arquivo `app/app.module.ts`. Vamos dar uma olhada neste arquivo.

A última linha no arquivo define uma classe JavaScript:

```js
export class AppModule {}
```

`export` é uma palavra reservada em JavaScript que informa que tudo o que for definido depois deve ser exposto a outros arquivos que importam isto usando a instrução `import`. Você pode ver exemplos de classes importadas de outros arquivos nas primeiras linhas deste arquivo.

A classe `AppModule` está vazia. Obterá a sua funcionalidade do Angular, que identificará seu papel pelo código anterior a esta linha, começando por `@NgModule ({`.

Toda entidade em Angular (ngModule, componentes, serviços, diretivas e pipes) é apenas uma classe **com um decorador**. O decorador diz a Angular qual é o papel desta classe.

`@NgModule ({...})` é um decorador. Um decorador é apenas uma função. Ao usá-lo, colocamos `@` antes do seu nome. Desta forma, torna-se um decorador: ele analisa o que está escrito logo após a chamada da função e o recebe como um argumento. Os decoradores geralmente fazem algo com o que decoram. Nesse caso, por exemplo, `ngModule` recebe a classe `AppModule` e adiciona aos métodos e membros que mais tarde serão usados pelo Angular. Desta forma, Angular reconhecerá que esta classe representa um ngModule.

O que passamos pela função do decorador é usado pelo Angular para decorar a classe. Você pode ver que nós passamos um objeto com membros, cada membro é uma lista de outras classes. Nós vamos explicar rapidamente o que cada membro representa.

**declarações**: uma lista de coisas do Angular que são relevantes neste módulo. Elas podem usar umas as outras. Por exemplo, uma diretiva usada em um componente. Nós passamos aqui somente um componente - `AppComponent`, porque é só o que temos na nossa aplicação agora.

**imports**: uma lista de outros NgModules que são necessários para este módulo. Por exemplo, nós podemos usar coisas do `FormsModule` - diretivas e serviços, dentro de `AppComponent`.

**bootstrap**: este membro é relevante apenas para o ngModule raiz. Você não o encontrará nos módulos da lista de importações, por exemplo. Ele diz a Angular qual componente deve ser usado como o componente raiz da aplicação. Cada componente pode usar outros componentes em seu template. Temos um componente raiz que inicia toda a estrutura. Então nós realmente temos uma **estrutura de árvore** dos componentes que compõem nossa aplicação. Nesse caso, o componente raiz é `AppComponent` (com o seletor `app-root`). Vimos isso usado em `index.html` como o único componente dentro do `<body>`.

Como o Angular sabe que o `AppModule` é o ngModule raiz? Isso é definido no arquivo `main.ts` na última linha:

```js
platformBrowserDynamic()
  .bootstrapModule(AppModule)
  .catch(err => console.log(err));
```

Nós inicializamos nosso ngModule de raiz para um renderizador. Desta forma, contamos ao Angular o que o ngModule deve usar como ponto de partida da nossa aplicação. E também escolhemos um renderizador: `platformBrowserDynamic`. Ele sabe como levar nosso código e adicionar os dados relevantes (elementos, atributos, etc. ) ao DOM do navegador.

Se houver um erro, ele será capturado e registrado no console do navegador (visto quando as ferramentas de desenvolvimento do navegador estiverem abertas).

Podemos usar um renderizador diferente neste ponto, por exemplo, um que renderiza para elementos nativos do Android ou iOS! Nós só precisamos de um processador que conheça os nossos templates (que usam as notações HTML) e o código JavaScript e criam elementos nativos da aplicação móvel. Um exemplo desse renderizador é o [NativeScript](https://www.nativescript.org/) da Telerik.

Há até renderizadores para o Arduino, com os quais você pode conectar sensores, botões, LEDs e outro hardware à sua aplicação! Você pode ver um ótimo exemplo para isso aqui: [Building Simon with Angular2-IoT](https://medium.com/@urish/building-simon-with-angular2-iot-fceb78bb18e5#.430qu216w)

Nós vimos como dizemos ao Angular onde e como começar seu trabalho, como definimos o módulo raiz e o componente raiz, e como usamos o componente raiz.

No próximo capítulo, veremos como um componente está definido em Angular.
