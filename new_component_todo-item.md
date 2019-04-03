# Novo componente todo-item

Vamos criar um novo componente que será usado para cada item que é exibido na lista. Será um componente simples no começo, mas irá crescer
posteriormente. O que é importante é que **ele receberá o todo item como uma entrada para o componente pai**. Deste modo poderá ser um componente reusável, e não depende da aplicação diretamente.

Criaremos um novo componente chamado `item`: 

```
ng g c item -it
```

Você pode ver uma nova pasta criada com os arquivos  do componente.

Use o componente  no template do `appComponent` - dentro do elemento `<li>`:

```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item></todo-item>
  </li>
</ul>
```

Confira o resultado no navegador. O que você vê? Por que?

## @Input()
Nós queremos exibir o título de cada item dentro do componente `todo-item`. Precisamos passar o titulo atual do item no loop(ou o item inteiro) para o o componente `todo-item`. 

Novamente, Angular faz com que seja muito fácil para nós, fornecendo-nos o decorator `Input`.

Dentro da classe recém criada `itemComponent` (itemComponent) adicione a linha:
```ts
@Input() itemTitle: string;
```
Ele diz ao componente que espera uma entrada do tipo string e atribui ao membro da classe chamada `itemTitle`. Certifique-se  de que o `Input` seja adicionado à declaração de importação na primeira linha do arquivo. Agora, podemos usá-lo  dentro do template `itemComponent`:
```html
{{ itemTitle }}
```

Você pode adicionar qualquer outro elemento HTML que você gostaria aqui.

Agora precisamos passar uma String, qual é o título do item, onde nós usamos o componente. Volte ao `appComponent` e passe o titulo do item ao `todo-item`:
```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item [itemTitle]="item.title"></todo-item>
  </li>
</ul>
```

O `itemTitle` entre colchetes é o mesmos que foi declarado como componente no `@Input`.

Nós usamos a propriedade Binding em um elemento que nós mesmos criamos! E agora podemos realmente ver e entender que a vinculação da propriedade Binding se liga a propriedade atual do componente.

## Passando o item inteiro
Vamos refatorar um pouco o nosso código para que possamos facilmente implementar mais funcionalidades no componente `todo-item`, por exemplo, editando e removendo o item. Em vez de passar apenas o título ao componente, poderíamos passar todo o item, e deixar o componente extrair o título quando necessário.

No `itemComponent` mudamos a interpolação no template para:
```html
{{ todoItem.title }}
```
Renomeamos o Input e mudamos o tipo:
```ts
@Input() todoItem: any;
```

Agora passamos todo o item à propriedade renomeada no `appComponent` (retire o .title):
```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item [todoItem]="item"></todo-item>
  </li>
</ul>
```

Agora temos uma lista de componentes, então cada componente recebeu seus dados de um loop do componente pai. Agora, veremos  como esta lista pode ser dinâmica.
