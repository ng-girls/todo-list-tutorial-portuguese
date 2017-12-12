# Adicionando mais habilidades ao serviço

# Neste capítulo nós iremos melhorar nosso serviço adicionando novas habilidades.

Primeiro, vamos abrir o arquivo de serviço do nosso app que está disponível em `app/todo-list.service.ts`

Lá, iremos adicionar uma nova função ao serviço, chamada addItem, como demonstrado abaixo:
```javascript
addItem(item): void { 
    this.todoList.push(item); 
} 
```

Isso irá permitir que o aplicativo chame a mesma função em qualquer lugar da aplicação deixando nosso app mais fácil de manter.

Agora nós podemos mudar nosso código em `app/list-manager/list-manager.component.ts` para chamar a função `addItem` diretamente do serviço, como: 

```javascript
addItem(item): void { 
    this.todoListService.addItem(item); 
} 
```

- Pode ser necessário utilizar lógica adicional quando esses métodos forem chamados no DB (nós iremos implementar isso mais tarde)
- É considerado um jeito melhor de lidar com dados se os objetos forem imutáveis, assim não haverão ligações - as referências irão mudar (porém nós não iremos implementar redux nesse tutorial agora).


