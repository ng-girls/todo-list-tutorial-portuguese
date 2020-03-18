# \#16: 🎁 Adicionando itens usando Service

Vamos melhorar nosso serviço adicionando mais recursos que serão utilizados pelos nossos componentes. Primeiro - nós vamos implementar adicionar um item à lista.

## Adicionando um item

Vamos adicionar um novo método ao serviço chamado `addItem`, dessa forma:

{% code title="src/app/services/todo-list.service.ts" %}
```typescript
addItem(item: TodoItem) { 
  this.todoList.push(item);
}
```
{% endcode %}

Agora nós podemos alterar nosso componente `list-manager` para chamar o método `addItem` diretamente do serviço:

{% code title="src/app/list-manager/list-manager.component.ts" %}
```typescript
addItem(title: string) {
    this.todoListService.addItem({ title });
}
```
{% endcode %}

* Observe que o método do serviço espera o item inteiro, enquanto o método do componente espera apenas o título \(tittle\) e constrói o item. \(Você pode decidir deixar o serviço construir o item a partir do título\);
* Pode haver uma lógica adicional ao chamar estes métodos, por exemplo, salvando as alterações em um banco de dados \(que nós vamos implementar depois\);
* Uma melhor forma de manipular dados é utilizando _objetos imutáveis_ \(immutable objects\), mas este é um tópico maior do que podemos abordar no tutorial nesse momento.

{% hint style="success" %}
[See the results on StackBlitz](https://stackblitz.com/github/ng-girls/todo-list-tutorial/tree/master/examples/16-add-items-using-the-service)
{% endhint %}
