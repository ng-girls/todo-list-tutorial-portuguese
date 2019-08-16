# \#3: 📐 Component

Uma abordagem em desenvolvimento Web \(e desenvolvimento de software em geral\) é a arquitetura baseada em componentes (component-based architecture). No passar dos anos isso ganhou muita popularidade. O que é um componente? 

Helmut Petritsch define em [Service-Oriented Architecture \(SOA\) vs. Component Based Architecture](http://petritsch.co.at/download/SOA_vs_component_based.pdf):

> Um componente é um objeto de software, feito para interagir com outros componentes, encapsulando certas funcionalidades ou um conjunto de funcionalidades. Um componente possui uma interface claramente definida e está em conformidade com um comportamento prescrito comum a todos os componentes dentro de uma arquitetura.

Em aplicações Web, **um componente controla um fragmento de tela chamado de View (visualização)**. É uma parte do que você vai eventualmente ver na tela. Tem um template, no qual define sua estrutura visual. Também tem uma lógica no qual define o comportamento e os valores dinâmicos. A parte lógica é código Javascript e é chamado de controlador. 

Aqui está o diagrama de um componente em Angular, com o resultado abaixo. 
![](assets/component_angular2.png)

Diretivas, pipes e serviços são outros blocos de construção em Angular, no qual vamos discutir mais tarde neste tutorial. 

Vamos dar uma olhada no componente que foi criado em Angular-CLI. Todos os arquivos relevantes estão na pasta `src/app`. Abra o arquivo `app.components.ts`.

Igual ao ngModules que nós vimos no capitulo anterior, um componente é também definido por uma classe com um decorador. Está é a definição da classe:
{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```typescript
export class AppComponent {
  title = 'todo-list';
}
Tem um membro chamado "`title`". É uma variável no qual você pode atribuir um valor. O valor atribuído aqui é a string "todo funciona!".

O Angular cuida da sincronização dos membros do componente com o componente template. Então podemos usar facilmente o membro `title` no template. Dê uma olhada no template anexado ao componente em:

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.html" %}
```markup
<h1>
  Welcome to {{ title }}!
</h1>
```
{% endcode-tabs-item %}
{% endcode-tabs %}
As chaves duplas e seu conteúdo são chamados de [**Interpolação**](https://angular.io/guide/glossary#interpolation). Isso é uma das formas de **data binding** em Angular. Como nós mencionamos anteriormente, o código neste arquivo não é usado como quando o navegador renderiza o componente. Angular compila isso para o código Javascript. Em um dos passos de compilação ele procura pela Interpolações dentro do template. **O conteúdo da interpolação é uma expressão, escrita em Javascript.** Em tempo de execução a expressão é avaliada, e aí você vê o resultado. 

Interpolação é uma das mais fortes e mais básicas características em Angular. Existe desde o início do Angular - na primeira versão. Isso torna realmente simples a inserção de dados dinâmicos no View.  

Neste componente, a expressão é simplesmente o membro da classe do componente, `title`. **Vamos tentar mudar isso**. Tente o que está a seguir e veja o resultado no navegador. \(Com cada mudança que você faz no arquivo, o navegador vai atualizar automaticamente!\)

* Remova as chaves e mantenha o conteúdo `title`
* Coloque de volta as chaves e substitua o conteúdo com algum tipo de expressão matemática, por exemplo: `{% raw %}{{ 2 + 2 }}{% endraw %}`. \(Os espaços não são mandatórios, eles apenas deixam o código mais legível.\)
* Escreva uma expressão matemática combinada com o membro `title`: `{% raw %}{{ title + 10 }}{% endraw %}`
* Passe uma variável indefinida para a expressão - uma variavel na qual não foi declarada na classe do componente. Por exemplo: `{% raw %}{{ x }}{% endraw %}`
* Tente qualquer coisa que você gostaria. Não se preocupe - Você não vai fazer nada de mal para o navegador no seu computador! No pior caso, o navegador vai ficar sem memória e vai travar. \(Mas você tem que escrever algo realmente complicado para fazer isso acontecer!\)

Esse é o um dos caminhos em que você pode ligar membros dos componentes do controlador ao seu template. Como o Angular realmente sabe que isso é um template do componente do App?

Vamos voltar atrás no arquivo `app.component.ts` e ver a meta-data do componente definida no decorador `@Component` bem acima da definição da classe:
{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```typescript
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
```
{% endcode-tabs-item %}
{% endcode-tabs %}
```
Nós passamos um objeto de definições para o decorador, igual nós vimos no capitulo anterior com o ngModule. O segundo proprietário, `templateUrl` diz para o Angular onde procurar pelo template anexado ao componente. Há uma outra opção para apontar para o template, no qual é uma melhor prática: Escreva o template inteiro inline aqui, no componente de definição. Nós vamos discutir isso mais tarde.

A terceira propriedade, `styleUrls` diz ao Angular onde procurar pelos arquivos de CSS que definem o estilo desse componente. Pode ter múltiplos arquivos CSS. É por isso que o valor do `styleUrls` é um array. Você pode dar uma olhada no arquivo de CSS `app.component.css` - você vai encontra-lo vazio. Você pode adicionar um pouco de CSS aqui, por exemplo: 

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.css" %}
```css
h1 {
  color: red;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Nós vamos adicionar mais estilos mais pra frente. 

A primeira propriedade, `selector`, diz ao Angular qual será o nome da tag que nós vamos usar para chamar o componente. Como nós vimos no arquivo `src/index.html`, nós vamos usar o componente do App dentro do body:

{% code-tabs %}
{% code-tabs-item title="src/index.html" %}
```markup
<body>
  <app-root></app-root>
</body>
```
{% endcode-tabs-item %}
{% endcode-tabs %}
O Elemento `todo-root` não é um elemento HTML. É o componente que foi criado com o seletor `todo-root`. Tente mudar o seletor. Você vai ver isso se você mudar apenas um dos arquivos, "Carregando..." será mostrado. Esse é o conteúdo que nós queremos dar para a tag no `index.html`, e será renderizado com tanto que o elemento não seja substituído com um componente do Angular. Você pode ver no console do navegador uma mensagem de erro. 

Uma última coisa, a primeira linha do componente importa o código que define o decorador `@Component`. Ele precisa usar o decorador, no qual é definido no arquivo importado \(ou na verdade, em um dos seu próprios importadores\). Tente remover essa linha e veja o erro. 

#### Inline Template
Vamos mover o template para que seja **inline** na definição do componente. Isso vai nos ajudar a gerenciar o template enquanto olhamos sua funcionalidade.
No arquivo `app.component.ts` substitua a linha

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```typescript
templateUrl: './app.component.html',
```
{% endcode-tabs-item %}
{% endcode-tabs %}

with

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```typescript
template: ``,
```
{% endcode-tabs-item %}
{% endcode-tabs %}


Repare que usamos **crases** (ou *backticks*) ao invés de aspas simples - esta é uma nova forma para fazer templates literais (ou template strings), que foi lançada no JavaScript novo \(ES6\). Dessa forma você pode escrever uma string com múltiplas linhas, e funcionalidade legal é usar facilmente variáveis JavaScript e expressões dentro da string \(sem relação com expressões de binding do Angular no template\). Leia sobre isso na [documentação MDN](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Template_literals).

Tenha certeza de que substituiu o `templateUrl` com `template` e não se esqueça da vírgula no fim da linha. 

Agora copie o template inteiro do `app.component.html` e cole entre os backticks. Nós vamos formatar o código um pouco para ficar mais legível:
{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```markup
template: `
  <h1>
    Welcome to {{ title }}!
  </h1>  
`,
```
{% endcode-tabs-item %}
{% endcode-tabs %}


É mais fácil de entender o template quando nós vemos a classe (controller) ao mesmo tempo. Porém usamos isto apenas quando o template é simples e pequeno, ou quando a classe não é muito complicada. Se a classe começar a ficar grande, é um sinal de que você deve refatorar seu código quebrando em componentes filho. 

Nesse ponto você pode deletar o arquivo `app.component.html`.

** Recomendamos continuar este tutorial usando modelos embutidos nos componentes. ** Especialmente se você estiver trabalhando em um laptop com uma tela pequena, onde não há espaço suficiente para abrir dois arquivos lado a lado.

Vamos configurar a CLI Angular para nos fornecer um modelo interno como padrão. No terminal, execute o comando: `ng config schematics. @ Schematics / angular.component.inlineTemplate true`. Agora, todos os componentes que você irá gerar terão um modelo embutido, e um arquivo HTML não será criado.

Se você deseja continuar este tutorial com templates em arquivos HTML separados, não execute este comando, e use os arquivos `.html` gerados para os templates.

> **Background:** Você pode especificar que gostaria de usar o modelo inline em todo o projeto de várias maneiras:
>
> * Ao gerar um projeto, passe a bandeira `-it` ou` --inline-template` assim: `ng new todo-list -it`
> * Depois de gerar um projeto, adicione-o à configuração para que os componentes gerados a partir desse ponto tenham um modelo in-line: `ng config projects.YOURPROJECTNAME.schematics. @ Schematics / angular: component.inlineTemplate true`. Isso adiciona a linha `inlineTemplate: true` no arquivo de configuração Angular CLI` angular.json`. Você também pode editar o arquivo diretamente.
> * Se você não configurou para ter templates embutidos como padrão, você pode especificar isto por componente quando você os gerar, passando o sinalizador `-it` ou` --inline-template`. Por exemplo: `ng generate header -it`.

Da mesma forma que usamos o modelo in-line, também podemos usar estilos in-line. Mas por enquanto vamos manter os estilos em um arquivo separado.

{% hint style="info" %}
**Instruções StackBlitz** ![](assets/stackblitz-hint.svg)


O StackBlitz não suporta a configuração de modelo inline. Nós precisaremos mover manualmente o código do template do arquivo `.html` para o arquivo` .component.ts` toda vez que criarmos um novo componente. Não se preocupe! Apenas observe o painel de informações das instruções do StackBlitz e nós o orientaremos.
{% endhint %}

### Sumário
Exploramos o componente `root` (raiz) que foi gerado por nós através da CLI, e refatoramos alguns pontos. No próximo capítulo vamos criar um novo componente, e vamos iniciar a árvore de componentes, no qual define a estrutura da aplicação. 

{% hint style="success" %}
[Veja os resultados no StackBlitz](https://stackblitz.com/github/ng-girls/todo-list-tutorial/tree/master/examples/03-component )
{% endhint %}
