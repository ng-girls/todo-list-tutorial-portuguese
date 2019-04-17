# \#17: 💾Armazenamento Local

Nós gostariamos de manter a lista de tarefas em nosso computador para que, ao acessar ou recarregar o app, possamos ver a lista com as alterações que fizemos. Idealmente, a lista deveria ser salva em um banco de dados, mas iremos implementar uma versão simples usando o próprio armazenamento do navegador.

## O que é armazenamento local?

Armazenamento Local (do inglês local storage), como sugere o nome, é uma ferramenta para armazenar dados localmente. Tão similar quanto os cookies, o armazenamento local armazena os dados no computador do usuário, e por isso nos permite, como desenvolvedores, um jeito mais rápido de acessar esses dados tanto para leitura e escrita.

> Existem bibliotecas que você pode usar que oferecem uma grande variedade de métodos genéricos e robustos para gerenciar os dados no armazenamento local. Aqui iremos implementar uma solução simples.

## Suporte ao Navegador 

Como o armazenamento local nos foi apresentado pela primeira vez juntamente com o HTML5, todos os navegadores que suportam o padrão HTML5 também irão comportar o armazenamento local. Basicamente é suportado pela maioria dos web browsers modernos, incluindo o IE 8.

## Queremos ver um pouco de código!

Primeiro, para usar o armazenamento local, podemos simplesmente acessar a uma instância do `localStorage` a qual está exposta para nós globalmente. 
Isso significa que podemos chamar todos os métodos disponíveis nessa interface simplesmente usando essa instância. 

O armazenamento local guarda os dados no formato chave-valor, logo a interface é bastante simples e possui dois métodos principais: `getItem` e `setItem`.

Um exemplo de uso:

{% code-tabs %}
{% code-tabs-item title="code for example" %}
```typescript
localStorage.setItem('name','Angular');

let name = localStorage.getItem('name'); 
alert(`Hello ${ name }!`);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Outro método útil é o `clear`. Ele é usado para limpar o armazenamento local de dados:

{% code-tabs %}
{% code-tabs-item title="code for example" %}
```typescript
localStorage.clear();
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Há mais outros métodos maravilhosos que você pode usar, como descritos no [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/Storage).

## Hora do Angular \(de volta ao nosso app\)

Na seção a seguir vamos construir um serviço de armazenamento local que mais tarde será usado para armazenar os itens da nossa lista de tarefas. Será um serviço genérico de listagem de objetos. Precisamos informar o nome do dado que estamos procurando \(uma chave (key)\), para que possamos usá-lo para armazenar outras listas também.

Como foi dito nos capítulos anteriores, vamos gerar um serviço usando o Angular CLI. Vamos nomear o novo serviço `storage`:

```bash
ng g s services/storage
```

O novo arquivo `storage.service.ts`, deve ser criado com o código abaixo:

{% code-tabs %}
{% code-tabs-item title="src/app/services/storage.service.ts" %}
```typescript
import { Injectable } from '@angular/core';

@Injectable()
export class StorageService {

  constructor() { }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Se algo está lhe parecendo estranho, por favor consulte o [Capítulo: Criar um Serviço](creating-a-service.md) para mais informações detalhadas sobre serviços.

Precisamos fornecer o serviço em nosso ngModule. Abra `app.module.ts` e na lista de `providers` list adicione a nova classe:

{% code-tabs %}
{% code-tabs-item title="src/app/app.module.ts" %}
```typescript
providers: [
  TodoListService, 
  StorageService
],
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Certifique-se de que a classe também foi importada para o arquivo:

{% code-tabs %}
{% code-tabs-item title="src/app/app.module.ts" %}
```typescript
import { StorageService } from './services/storage.service';
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Como não podemos acessar um item na lista diretamente no armazenamento local, implementaremos apenas dois métodos: obter os dados e salvar os dados. Mudar a lista será feito pelo TodoListService. Para cada método, vamos passar a chave (nome) dos dados que queremos.

### getData

Este método irá pegar e retornar os dados \(objetos, lista, etc.\) armazenados no serviço sob a chave:

{% code-tabs %}
{% code-tabs-item title="src/app/services/storage.service.ts" %}
```typescript
  getData(key: string): any {
    return JSON.parse(localStorage.getItem(key));  
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Espera! Espera! Por que`JSON.parse`? A resposta é simples:
Conforme descrito anteriormente nesse tutorial, o armazenamento local memoriza os dados em uma forma de chave-valor, isso significa que os valores são armazenados como **strings**.
Então, se quisermos ter um objeto real \(ou lista\) para tratar, devemos converter a string em um objeto JavaScript válido.

### setData

Este método irá salvar os dados \(objeto, lista, etc.\) fornecidos sob uma chave \(key\)

{% code-tabs %}
{% code-tabs-item title="src/app/services/storage.service.ts" %}
```typescript
  setData(key: string, data: any) {
    localStorage.setItem(key, JSON.stringify(data));
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

É isso! Vamos usar esse serviço em nosso `ToDoListService`.

> Como mencionado anteriormente, este serviço poder ter uma API mais ampla com métodos mais robustos. Quando se escreve um serviço para acessar um banco de dados, existe outros métodos para adicionar, modificar e excluir itens especifícos.

## Usando o ListStorageService

Nós gostaríamos de usar o seriço recém-criado de dentro do `TodoListService`. Primeiro precisaremos injetar o `StorageService` no `TodoListService`, assim como injetamos no `ListManagerComponent`. Vamos pedir por uma instância do serviço no construtor e garantir que a sua classe seja importada. Vamos mover a lista de tarefas padrão para fora da classe. Também iremos adicionar uma constante com a chave do nosso armazenamento.

> Uma boa prática é usar os arquivos de ambientes para armazenar as chaves. Dessa forma, é possível gerenciar diferentes chaves para cada ammbiente - desenvolmento, produção, staging, etc.

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
import { Injectable } from '@angular/core';
import { TodoItem } from '../interfaces/todo-item';
import { StorageService } from './storage.service';

const todoListStorageKey = 'Todo_List';

const defaultTodoList = [
  {title: 'install NodeJS'},
  {title: 'install Angular CLI'},
  {title: 'create new app'},
  {title: 'serve app'},
  {title: 'develop app'},
  {title: 'deploy app'},
];

@Injectable()
export class TodoListService {
  todoList: TodoItem[];

  constructor(private storageService: StorageService) { }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Vamos manter uma versão em tempo de execução da lista de tarefas no serviço para nos ajudar a gerenciá-lo no aplicativo - a propriedade `todoList`. Vamos inicializá-lo no construtor com a lista no armazenamento local, se existir, ou então com lista a padrão.

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
constructor(private storageService: StorageService) {
  this.todoList = 
    storageService.getData(todoListStorageKey) || defaultTodoList;
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Agora iremos implementar os métodos para gerenciar nossa lista.

### Adicionar um item (addItem)

Vamos adicionar um item na lista de tarefas \(igual foi feito anteriormente\) e então atualizar o armazenamento.

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
addItem(item: TodoItem) {
  this.todoList.push(item);
  this.storageService.setData(todoListStorageKey, this.todoList);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Atualizar um item (updateItem)

Aqui queremos atualizar um item existente. Vamos supor que mantemos o item original por referência e podemos encontrá-lo na lista. \(Outras implementações podem usar um ID do item para pesquisar na lista.\) Depois, vamos substituí-lo por uma nova versão. Finalmente, atualizaremos o armazenamento.

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
updateItem(item: TodoItem, changes) {
  const index = this.todoList.indexOf(item);
  this.todoList[index] = { ...item, ...changes };
  this.storageService.setData(todoListStorageKey, this.todoList);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Então o que está acontecendo aqui?
Nós localizamos o item na lista. Em seguida, no mesmo local, atribuímo um novo objeto, que é construído a partir do item original e das alterações feitas nele. Estamos usando o operador spread para isso: um novo objeto é construído, composto pelo conjunto original de chaves-valores \(`...item`\) que são substituídos pelas chaves-valores de `changes`. \(Se uma chave em `changes` não existe em `item`, ela é adicionada ao novo objeto.\)

### DRY - Don't Repeat Yourself (Não repita você mesmo)

Você pode ter notado que temos a mesma linha de código em `addItem` e `updateItem`:

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
this.storageService.setData(todoListStorageKey, this.todoList);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Gostaríamos de reduzir a repetição de código e extrair o código repetido em um método. Você pode usar o IDE para ajudá-lo a extrair o método. Selecione a linha a cima, clique com o botão direito e procure a opção para refatorar extraindo um método. O método extraído deve ficar assim:

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
saveList() {
    this.storageService.setData(todoListStorageKey, this.todoList);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Agora, certifique-se de chamar `saveList` de dentro dos métodos `addItem` e `updateItem`.

### Deletar item (deleteItem)

Este método vai remover um item da lista. Nós procuramos pelo item na lista, remove, e então salva as alterações.

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
deleteItem(item: TodoItem) {
  const index = this.todoList.indexOf(item);
  this.todoList.splice(index, 1);
  this.saveList();
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

`splice(i, n)` remove `n` itens começando pelo index `i`. Em nosso código, nós removemos somente um item \(é por isso que usamos 1 como segundo parâmetro\).

### Resultado final

Nosso TodoListService está pronto com métodos para obter e modificar a lista de tarefas. Podemos usar esses métodos dos componentes.

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
import { Injectable } from '@angular/core';
import { TodoItem } from '../interfaces/todo-item';
import { StorageService } from './storage.service';

const todoListStorageKey = 'Todo_List';

const defaultTodoList = [
  {title: 'install NodeJS'},
  {title: 'install Angular CLI'},
  {title: 'create new app'},
  {title: 'serve app'},
  {title: 'develop app'},
  {title: 'deploy app'},
];

@Injectable()
export class TodoListService {
  todoList: TodoItem[];

  constructor(private storageService: StorageService) {
    this.todoList = 
      storageService.getData(todoListStorageKey) || defaultTodoList;
  }

  saveList() {
    this.storageService.setData(todoListStorageKey, this.todoList);
}

  addItem(item: TodoItem) {
    this.todoList.push(item);
    this.saveList();
  }
  
  updateItem(item, changes) {
    const index = this.todoList.indexOf(item);
    this.todoList[index] = { ...item, ...changes };
    this.saveList();
  }
  
  deleteItem(item) {
    const index = this.todoList.indexOf(item);
    this.todoList.splice(index, 1);
    this.saveList();
  }

}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Resumo

Neste capítulo aprendemos o que é armazenamento local e como usá-lo.
Vimos que o `localStorage` é uma ótima e direta ferramenta para desenvolvedores armazenar dados localmente nos computadores/dispositivos dos usuários.
Nós então implementamos um novo serviço que usa o `localStorage` para guardar os dados que nosso `TodoListService` usa para salvar os itens da lista de tarefas.