# \#9: 📋 A lista de tarefas

Agora, você vai adicionar a todo-list ao componente `app-root`. Abra o arquivo `src/app/app.component.ts`. Adicione a lista de itens dentro da classe `AppComponent` como um array de objetos para cada item. Nesta fase cada item conterá apenas um título:

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```typescript
export class AppComponent {
  title = 'app';
  todoList = [
    {title: 'install NodeJS'},
    {title: 'install Angular CLI'},
    {title: 'create new app'},
    {title: 'serve app'},
    {title: 'develop app'},
    {title: 'deploy app'},
  ];
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

> Colocar informação \(recursos\) dentro do seu código é chamado hardcoding e é considerada uma má prática. Eventualmente obteremos a lista de um recurso externo, mas, mesmo que não seja, é melhor colocar dados simulados em seus próprios arquivos. Mas vamos avançar passo-a-passo, então definir itens dessa forma é uma boa alternativa para o momento.

Agora, você tem que dizer ao navegador para exibir esses itens. Para isso, você usará a **diretiva Angular,** `*ngFor`. Ela trabalha como uma estrutura de repetição em Java.  `*` é uma notação semântica necessária que faz com que o Angular use o elemento atual como template quando renderizar a lista.


Insira o loop logo após `<app-input-button-unit></app-input-button-unit>`, dessa forma:

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```markup
template: `
  <h1>
    Welcome to {{ title }}!
  </h1>

  <app-input-button-unit></app-input-button-unit>

  <ul>
    <li *ngFor="let todoItem of todoList">
      {{ todoItem.title }}
    </li>
  </ul>
`,
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Isso significa "percorrer todos itens do array todoList definido abaixo, e imprimir uma lista não numerada que contém os títulos dos itens". Ao percorrer a `todoList`, cada item é atribuído à variável `item`, e nós podemos usar esta variável dentro do elemento `li` e seus filhos.


### Diretivas angular

Diretivas são pedaços de lógica \(escritos como classes\) que podem ser anexadas a elementos e componentes. Elas são usadas para mudar a visualização ou o comportamento do elemento. O Angular já possui algumas diretivas incorporadas. 

Como nós vimos, a diretiva `ngFor` modifica o template em tempo de execução repetindo o elemento chamado e seu conteúdo. Outra diretiva, por exemplo, é o `ngIf`, que recebe uma expressão booleana. Apenas se a expressão for verdadeira, o Angular renderiza o elemento e seu conteúdo. Ela também necessita do prefixo `*` porque usa o elemento como um template, semelhante a diretiva `*ngFor`. Por exemplo:

{% code-tabs %}
{% code-tabs-item title="code for example" %}
```markup
<h1 *ngIf="userLoggedIn">Welcome!</h1>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Neste exemplo, `userLoggedIn` deve fazer parte do componente, e ter um valor verdadeiro ou falso. Se for verdadeiro, o elemento `h1` será exibido. Se for falso, o elemento não existirá no DOM.

Existem outras diretivas em Angular que não são estruturais \(e são usadas sem o `*`\). Por exemplo `ngStyle` e `ngClass`, que você pode aplicar estilo e classe dinamicamente ao elemento.
