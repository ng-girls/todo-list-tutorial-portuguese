# A lista

Agora, você vai adicionar a todo-list ao componente `app-root`. Abra o arquivo `src/app/app.component.ts`. Adicione a lista de items dentro da classe `AppComponent` como um array de objetos para cada item. Nesta fase cada item conterá apenas um título:

```js
todoList = [
  {title: 'install NodeJS'},
  {title: 'install Angular CLI'},
  {title: 'create new app'},
  {title: 'serve app'},
  {title: 'develop app'},
  {title: 'deploy app'},
];
```

> Colocar informação \(recursos\) dentro do seu código é chamado hardcoding e é considerada uma má prática. Eventualmente obteremos a lista de um recurso externo, but even if not it's best to mock data in their own files. Mas vamos avançar passo-a-passo, então definir items dessa forma é uma boa alternativa para o momento.

Agora, você tem que dizer ao navegador para exibir esses items. Para isso, você usará a **diretiva Angular, `*ngFor`**. Ela trabalha como uma estrutura de repetição em Java.  `*` é uma notação semântica necessária que faz com que o Angular use o elemento atual como template quando renderizar a lista.


Insira o loop logo após `<todo-input></todo-input>`, dessa forma:

```html
<todo-input></todo-input>
<ul>
  <li *ngFor="let item of todoList">
    {{ item.title }}
  </li>
</ul>
```

Isso significa "percorrer todos items do array todoList definido abaixo, e imprimir uma lista não numerada que contém os títulos dos items". Ao percorrer a `todoList`, cada item é atribuído à variável `item`, e nós podemos usar esta variável dentro do elemento `li` e seus filhos.


### Diretivas angular

Diretivas são pedaços de lógica \(escritos como classes\) que podem ser anexadas a elementos e componentes. Elas são usadas para mudar a visualização ou o comportamento do elemento. O Angular já possui algumas diretivas incorporadas. 

Como nós vimos, a diretiva `ngFor` modifica o template em tempo de execução repetindo o elemento chamado e seu conteúdo. Outra diretiva, por exemplo, é o `ngIf`, que recebe uma expressão booleana. Apenas se a expressão for verdadeira, o Angular renderiza o elemento e seu conteúdo. Ela também necessita do prefixo `*` porque usa o elemento como um template, semelhante a diretiva `*ngFor`. Por exemplo:

```html
<h1 *ngIf="userLoggedIn">Welcome!</h1>
```

Neste exemplo, `userLoggedIn` deve fazer parte do componente, e ter um valor verdadeiro ou falso. Se for verdadeiro, o elemento será exibido. Se for falso, o elemento não existirá no DOM.

Existem outras diretivas em Angular que não são estruturais \(e são usadas sem o `*`\). Por exemplo ngStyle e ngClass, que você pode aplicar estilo e classe dinamicamente ao elemento.
