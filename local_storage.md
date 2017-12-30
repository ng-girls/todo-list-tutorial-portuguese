# Armazenamento Local

## O que é armazenamento local?

Armazenamento Local (do inglês local storage), como sugere o nome, é uma ferramenta para armazenar dados localmente. Tão similar quanto os cookies, o armazenamento local armazena os dados no computador do usuário, e por isso nos permite, como desenvolvedores, um jeito mais rápido de acessar esses dados tanto para leitura e escrita.

## Apoio do Browser 

Como o armazenamento local nos foi apresentado pela primeira vez juntamente com o HTML5, todos os navegadores que suportam o padrão HTML5 também irão comportar o armazenamento local. Basicamente é suportado pela maioria dos web browsers modernos, incluindo o IE 8.

## Queremos ver um pouco de código!

Primeiro, para usar o armazenamento local, podemos simplesmente acessar a uma instância do localStorage a qual está exposta para nós globalmente. 
Isso significa que podemos chamar todos os métodos disponíveis nessa interface simplesmente usando essa instância. 

O armazenamento local guarda os dados no formato chave-valor, logo a interface é bastante simples e  possui dois métodos principais: `getItem` e `setItem`.

Um exemplo de uso:

```
localStorage.setItem('name','Mor');

let name = localStorage.getItem('name'); 
alert('Hello '+name+'!');
```
Outro método útil é o `clear` e é usado para limpar o armazenamento local de dados:

`localStorage.clear();`

Há mais outros métodos maravilhosos que você pode usar, como descritos [aqui](https://developer.mozilla.org/en-US/docs/Web/API/Storage).

## Hora do Angular \(de volta ao nosso app\)

Na seção a seguir vamos contruir um serviço de armazenamento local que mais tarde será usado para armazenar os itens da nossa lista de tarefas.
Como foi dito nos tutoriais anteriores, vamos gerar um serviço usando `angular-cli`:

```
ng g s todo-list-storage
```

O novo arquivo `todo-list-storage.service.ts`, deve ser criado com o código abaixo:

```
import { Injectable } from '@angular/core';

@Injectable()
export class TodoListStorageService {

  constructor() { }

}
```

**Se algo está lhe parecendo estranho, por favor consulte o [Tutorial do Serviço](https://shmool.gitbooks.io/todo-list-tutorial/content/service.html) para mais informações detalhadas sobre serviços.**

Precisamos fornecer o serviço em nosso ngModule. Abra`app.module.ts` e na lista de `providers` list adicione a nova classe:
```ts
providers: [TodoListService, TodoListStorageService],
```
Certifique-se de que a classe também foi importada para o arquivo:
```ts

import { TodoListStorageService } from './todo-list-storage.service';
```
Vamos começar adicionando uma propriedade privada para o nosso serviço `todoList` a qual irá conter os itens da lista. 

`private todoList;`

Além disso, vamos adicionar uma constante que irá armazenar o nome da chave que vamos usar para o nosso armazenamento local, adicione logo após as importações:

`const storageName = 'aah_todo_list';`

Agora queremos inicializar essa propriedade com dados, recuperando do localStorage, dentro do construtor, adicione:

```ts
constructor() {  
    this.todoList = JSON.parse(localStorage.getItem(storageName));  
}
```
Espera! Espera! Por que`JSON.parse`? A resposta é simples:
Conforme descrito anteriormente nesse tutorial, o armazenamento  local memoriza os dados em uma forma de chave-valor, isso significa que os valores são armazenados como **strings**.
Então, se quisermos ter um objeto real para tratar, devemos converter a string em um objeto válido.  

Agora vamos começar fazendo algumas coisas reais, mas primeiro iremos declarar todos os métodos públicos que queros expor nesse serviço, que são **get, post, put**, e **destroy**.  
Nosso serviço deve parecer algo similar à isso:

```
import { Injectable } from '@angular/core';

const storageName = 'aah_todo_list';

@Injectable()
export class TodoListStorageService {

  private todoList;

  constructor() {
    this.todoList = JSON.parse(localStorage.getItem(storageName));
  }

  // get items
  get() {}

  // add a new item
  post(item) {}

  // update an item
  put(item, changes) {}

  // remove an item
  destroy(item) {}

}
```

Nós iremos agora implementá-los um por um.

### get

Esse método irá simplesmente retornar o estado atual dos itens armazenados no serviço:

```
/**
   * get items
   * @returns {any[]}
   */
  get() {
    return [...this.todoList];
  }
```

Se você não está familiarizada com o operador  `...`, por favor verifique [essa documentação](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Spread_operator) para maiores informações.

### post

Esse método será responsável por adicionar um novo item e retornar a nova lista. Ele aceita um parâmetro,`item` o qual será o item a ser adicionado:

```
/**
   * Add a new todo item
   * @param item
   * @returns {any[]}
   */
  post(item) {
    this.todoList.push(item);
    return this.get();
  }
```

Algumas de vocês devem ter percebido que adicionamos um novo item no array. Mas e o armazenamento local? Devemos também sincronizá-lo com o novo array!

Vamos adicionar um novo método **privado** em nosso serviço, o qual será usado internamente para atualizar a lista armazenada:

```
/**
   * Sincroniza o armazenamento local com a lista atual
   * @returns {any[]}
   */
  private update() {
    localStorage.setItem(storageName, JSON.stringify(this.todoList));

    return this.get();
  }
```

Vamos explicar.  
Aqui utilizamos o simples método de `setItem`, o qual pega uma chave \(primeiro argumento\) e um valor de string \(segundo argumento\) e armazena-o no armazenamento local.  
Depois que atualizamos o valor, simplesmente retornamos a nova lista usando o método `get` que implementamos anteriormente.

Agora precisamos modificar nossa função `post` para usar o `update` assim tudo será sincronizado em harmonia:

```
/**
   * Adiciona um novo item ao todo 
   * @param item
   * @returns {any[]}
   */
  post(item) {
    this.todoList.push(item);
    return this.update();
  }
```

### put

Aqui queremos atualizar um item existente.
Antes disso, vamos adicionar outro método auxiliar privado`findItemIndex`, o qual simplesmente irá returnar o indíce de um item com a lista de array:
```
/**
   * encontra o indíce de um item no array
   * @param item
   * @returns {number}
   */
  private findItemIndex(item) {
    return this.todoList.indexOf(item);
  }
```

Agora, podemos usar `Object.assign` para atualizar um item existente:

```
/**
   * Atualiza um item existente
   * @param item
   * @param changes
   * @returns {any[]}
   */
  put(item, changes) {
    Object.assign(this.todoList[this.findItemIndex(item)], changes);
    return this.update();
  }
```

Então, o que está acontecendo aqui?
`Object.assign` pega um objeto alvo (target) \(primeiro argumento\) e objetos de origem (source)\(todo o resto do argumento \), e copia para o objeto alvo. 
Se uma propriedade existe tanto no target e no source, esse método irá subsitutir o valor antigo pelo novo.
Aqui queremos atualizar um item na lista, então primeiro encontramos o seu indíce no array e depois aplicamos as mudanças nele.  
Por fim, queremos sincronizá-lo com o armazanamento local \(`this.update`\) e retornar a nova lista.

### destroy

Esse método irá remover um item da lista e sincronizar com o armazenamento local:

```
/**
   * Remove um item da lista
   * @param item
   * @returns {any[]}
   */
  destroy(item) {
    this.todoList.splice(this.findItemIndex(item), 1);
    return this.update();
  }
```

O código acima é bastante simples.
`splice(i, n)` remove `n` itens começando pelo indíce `i`.  
No nosso código, primeiro encontramos o indíce do item para remové-lo e removemos apenas ele \(porisso usamos 1 como segundo parâmetro\).

## Adicionando alguns dados padrão

Vamos assumir que queremos que a nossa lista de tarefas tenha alguns dados padrão para iniciar.

Então podemos adicioná-lo modificando nosso serviço, adicionando na seção de constantes \(depois das importações\):

```
const defaultList = [
  { title: 'install NodeJS' },
  { title: 'install Angular CLI' },
  { title: 'create new app' },
  { title: 'serve app' },
  { title: 'develop app' },
  { title: 'deploy app' },
];
```

E, em seguida, modificar nosso construtor:

```
constructor() {
    this.todoList = JSON.parse(localStorage.getItem(storageName)) || defaultList;
  }
```

O código acima irá garantir que se os dados ainda não estiverem configurados para o localStorage, nosso serviço continuará tendo alguns dados padrões para retornar. 

## Quase lá!

Nosso serviço está pronto para funcionar!
Mas espere, precisamos fornecê-lo antes de usá-lo.

Abra o `app.module.ts` e adicione `TodoListStorageService` ao array de `providers`.  
Agora estamos realmente prontos para usar o serviço!

Agora para o nosso app usar o novo serviço de armazenamento local, vamos abrir o `todo-list.service.ts` e modificá-lo.

Primeiro precisamos importar o novo serviço:

`import { TodoListStorageService } from './todo-list-storage.service';`

Então, precisamos injeta-lo no construtor para que possamos ter uma instância para se trabalhar:

```
constructor(private storage:TodoListStorageService) {
}
```

Isso nos permitirá usar `this.storage` através do serviço do todo-list. 

Vamos também modificar os métodos a seguir:

**Antes**

```
getTodoList() {
    return this.todoList;
}

addItem(item) {
    this.todoList.push(item);
}
```

**Depois**

```
getTodoList() {
    return this.storage.get();
}

addItem(item) {
    return this.storage.post(item);
}
```

Agora temos uma última modificação para fazer. Abra o `list-manager.component.ts`, e vamos modificar o método `addItem` desse jeito:

```
addItem(title:string) {
    this.todoList = this.todoListService.addItem({ item:title });
}
```

A mudança acima irá garantir que quando adicionamos um item, nossa lista também será atualizada visualmente.

## Resumo

Neste tuturial aprendemos o que é armazenamento local e como usá-lo.
Vimos que o armazenamento local é uma ótima e direta ferramenta para desenvolvedores armazenar dados localmente nos computadores/dispositivos dos usuários.
Nós então implementamos um novo serviço que usa o armazenamento local para guardar os itens da lista de tarefas, e atualizamos o resto dos componentes para oferecer suporte esse novo serviço.

Aproveite o resto do tutorial!


