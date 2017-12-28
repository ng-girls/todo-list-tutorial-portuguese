# Component

Uma abordagem em desenvolvimento Web \(e desenvolvimento de software em geral\) é a arquitetura baseada em componentes (component-based architecture). No passar dos anos isso ganhou muita popularidade. O que é um componente? 

Helmut Petritsch define em [Service-Oriented Architecture \(SOA\) vs. Component Based Architecture](http://petritsch.co.at/download/SOA_vs_component_based.pdf):

> Um componente é um objeto de software, feito para interagir com outros componentes, encapsulando certas funcionalidades ou um conjunto de funcionalidades. Um componente possui uma interface claramente definida e está em conformidade com um comportamento prescrito comum a todos os componentes dentro de uma arquitetura.

Em aplicações Web, **um componente controla um fragmento de tela chamado de View (visualização)**. É uma parte do que você vai eventualmente ver na tela. Tem um template, no qual define sua estrutura visual. Também tem uma lógica no qual define o comportamento e os valores dinamicos. A parte lógica é código Javascript e é chamado de controlador. 

Aqui está o diagrama de um componente em Angular, com o resultado abaixo. 
![Angular 2 Component](Angular Component.001.jpeg)

Diretivas, pipes e serviços são outros blocos de construção em Angular, no qual vamos discutir mais tarde neste tutorial. 

Vamos dar uma olhada no componente que foi criado em Angular-CLI. Todos os arquivos relevantes estão na pasta `src/app`. Abra o arquivo `app.components.ts`.

Igual ao ngModules que nós vimos no capitulo anterior, um componente é também definido por uma classe com um decorador. Está é a definição da classe:
```js
export class AppComponent {
  title = 'todo funciona!';
}
```
Tem um membro chamado "titulo". É uma variavel no qual você pode atribuir um valor. O valor atribuido aqui é a string "todo funciona!".

O Angular cuida da sincronização dos membros do componente com o componente template. Então podemos usar facilmente o membro `title` no template. Dê uma olhada no template anexado ao componente em:

```html
<h1>
  {{ title }}
</h1>
```
As chaves duplas e seu conteúdo são chamados de **Interpolação**. Isso é uma das formas de ** data binding ** em Angular. Como nós mencionamos anteriormente, o código neste arquivo não é usado como quando o navegador renderiza o componente. Angular compila isso para o código Javascript. Em um dos passos de compilação ele procura pela Interpolações dentro do template. **O conteúdo da interpolação é uma expressão, escrita em Javascript.** Em tempo de execução a expressão é avaliada, e aí você vê o resultado. 

Interpolação é uma das mais fortes e mais básicas caracteristicas em Angular. Existe desde o inicio do Angular - na primeira versão. Isso torna realmente simples a inserção de dados dinâmicos no View.  

Nesse componente, a expressão é simplesmente o membro da classe do componente, `title`. **Vamos tentar mudar isso**. Tente o que está a seguir e veja o resultado no navegador. \(Com cada mudança que você faz no arquivo, o navegador vai atualizar automaticamente!\)

* Remova as chaves e mantenha o conteúdo `title`
* Coloque de volta as chaves e substitua o conteúdo com algum tipo de expressão matemática, por exemplo: `{% raw %}{{ 2 + 2 }}{% endraw %}`. \(Os espaços não são mandatórios, eles apenas deixam o código mais legível.\)
* Escreva uma expressão matemática combinada com o membro `title`: `{% raw %}{{ title + 10 }}{% endraw %}`
* Passe umaa variavel indefinida para a expressão - uma variavel na qual não foi declarada na classe do componente. Por exemplo: `{% raw %}{{ x }}{% endraw %}`
* Tente qualquer coisa que você gostaria. Não se preocupe - Você não vai fazer nada de mal para o navegador no seu computador! No pior caso, o navegador vai ficar sem memória e vai travar. \(Mas você tem que escrever algo realmente complicado para fazer isso acontecer!\)

Esse é o um dos caminhos em que você pode ligar membros dos componentes do controlador ao seu template. Como o Angular realmente sabe que isso é um template do componente do App?

Vamos voltar atrás no arquivo `app.component.ts` e ver a meta-data do componente definida no decorador `@Component` bem acima da definição da classe:
```js
@Component({
  selector: 'todo-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
```
Nós passamos um objeto de definições para o decorador, igual nós vimos no capitulo anterior com o ngModule. O segundo proprietário, `templateUrl` diz para o Angular onde procurar pelo template anexado ao componente. Há uma outra opção para apontar para o template, no qual é uma melhor prática: Escreva o template inteiro inline aqui, no componente de definição. Nós vamos discutir isso mais tarde.

A terceira propriedade, `styleUrls` diz ao Angular onde procurar pelos arquivos de CSS que definem o estilo desse componente. Pode ter multiplos arquivos CSS. É por isso que o valor do `styleUrls` é um array. Você pode dar uma olhada no arquivo de CSS `app.component.css` - você vai encontra-lo vazio. Você pode adicionar um pouco de CSS aqui, por exemplo: 

```css
h1 {
  color: red;
}
```

Nós vamos adicionar mais estilos mais pra frente. 

A primeira propriedade, `selector`, diz ao Angular qual será o nome da tag que nós vamos usar para chamar o componente. Como nós vimos no arquivo `src/index.html`, nós vamos usar o componente do App dentro do body:

```html
<body>
  <todo-root>Loading...</todo-root>
</body>
```
O Elemento `todo-root` não é um elemento HTML. É o componente que foi criado com o seletor `todo-root`. Tente mudar o seletor. Você vai ver isso se você mudar apenas um dos arquivos, "Carregando..." será mostrado. Esse é o conteúdo que nós queremos dar para a tag no `index.html`, e será renderizado com tanto que o elemento não seja substituido com um componente do Angular. Você pode ver no console do navegador uma mensagem de erro. 

Uma última coisa, a primeira linha do componente importa o código que define o decorador `@Component`. Ele precisa usar o decorador, no qual é definido no arquivo importado \(ou na verdade, em um dos seu próprios importadores\). Tente remover essa linha e veja o erro. 

#### Inline Template
Vamos mover o template para que seja **inline** na definição do componente. Isso vai nos ajudar a gerenciar o template enquanto olhamos sua funcionalidade.
No arquivo `app.component.ts` substitua a linha

```js
templateUrl: './app.component.html',
```

com

```js
template: ``,
```

Repare que **backticks** - eles são usados para definir literais de template, que é JavaScript novo \(ES6\). Dessa forma você pode definir multiplas linhas de string. Eles tem outra funcionalidade legal: usar facilmente variaveis JavaScript e expressões dentro da string \(sem relação com expressões de binding do Angular no template\). Leia sobre isso na [documentação MDN]
(https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Template_literals).

Tenha certeza de que substituiu o `templateUrl` com `template` e não se esqueça da vírgula no fim da linha. 

Agora copie o template inteiro do `app.component.html` e cole entre os backticks. Nós vamos formatar o código um pouco para ficar mais legivel:

```js
template: `
  <h1>
    {{ title }}
  </h1>  
`,
```

É mais fácil administrar o template quando nós vemos o controlador ao mesmo tempo. Isso é verdade com tanto que o template não fique muito grande e o controlador não fique muito complicado. Se ele ficar, é um sinal de que você deve refatorar seu código quebrando ele em componentes filho. 

Nesse ponto você pode deletar o arquivo `app.component.html`.
>Quando gerar um novo projeto, você pode definir o estado que você gostaria em um template inline para o componente raiz adicionando a flag `-it` (ou `--inline-template`). Tenha isso em mente para o próximo projeto. 

Da mesma forma nós usamos o template inline, nós também podemos usar estilos inline. Mas por enquanto vamos manter isso em um arquivo separado.

### Sumário
Nós exploramos o componente raiz que foi gerador por nós através do Angular-CLI, e até refatoramos. No próximo capitulo nós vamos criar um novo componente. Nós vamos iniciar a construir a arvore de componentes, no qua define a estrutura da aplicação. 
