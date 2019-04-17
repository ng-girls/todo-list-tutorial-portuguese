# \#11: ⛓ Interface

Queremos usar as habilidades do TypeScript para saber que tipo de objeto passamos como um `item` para o componente `todo-item`. Iremos ter certeza de que o item é do tipo certo. Mas o seu tipo não é uma simples string, número ou booleano. Vamos definir o tipo do item usando uma **interface**.

> Já vimos uma interface fornecida pelo Angular: a interface `OnInit`que inclui o método `ngOnInit`. Cada classe que implementa essa interface deve definir esse método. Caso contrário, obteremos um erro durante o tempo de compilação.
>
> Interfaces existem apenas no TypeScript e são removidas quando o código é compilado para JavaScript. Em JavaScript, não podemos impor a segurança do tipo.

Crie uma interface `TodoItem` em uma nova pasta chamada `interfaces` com o Angular CLI:

```bash
ng g i interfaces/todo-item
```

`i` é a contração para... você adivinhou - interface. Adicionando um caminho faz com que o Angular CLI gere as pastas que você indicou, se elas ainda não existirem.

Abra o arquivo recém criado `src/app/interfaces/todo-item.ts`:

{% code-tabs %}
{% code-tabs-item title="src/app/interfaces/todo-item.ts" %}
```typescript
export interface TodoItem {
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Agora, podemos definir que propriedades e/ou métodos cada objeto do tipo TodoItem deve ter. Neste ponto iremos adicionar dois métodos:

* `title` que deve ser do tipo `string`
* `completed` que é do tipo `boolean` e é um membro opcional

{% code-tabs %}
{% code-tabs-item title="src/app/interfaces/todo-item.ts" %}
```typescript
export interface TodoItem {
  title: string;
  completed?: boolean;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Vamos definir o item @Input para ser do tipo que criamos. Isso vai permitir que a IDE nos sugira membros disponíveis quando usarmos o item na classe e no modelo do componente.

{% code-tabs %}
{% code-tabs-item title="src/app/todo-item/todo-item.component.ts" %}
```typescript
export class TodoItemComponent implements OnInit {
  @Input() item: TodoItem;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Você vai precisar importar a interface nesse arquivo.

{% code-tabs %}
{% code-tabs-item title="src/app/todo-item/todo-item.component.ts" %}
```typescript
import { TodoItem } from '../interfaces/todo-item';
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Agora, vamos definir a lista de itens de tarefas para conter os objetos do tipo `TodoItem`

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```typescript
export class AppComponent {
title = 'app';
todoList: TodoItem[] = [
  {title: 'install NodeJS'},
  {title: 'install Angular CLI'},
  {title: 'create new app'},
  {title: 'serve app'},
  {title: 'develop app'},
  {title: 'deploy app'},
];
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Novamente, será preciso importar a interface para esse arquivo.

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```typescript
import { TodoItem } from './interfaces/todo-item';
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Agora tente excluir o título de um dos objetos na lista. O que acontece?