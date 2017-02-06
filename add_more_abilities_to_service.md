# Add more abilities to service

# In this chapter we would improve our service by adding more abilities.

First, lets open our app's service file which is available at - `app/todo-list.service.ts`

There we'll add a new function to the service, called `addItem`, like so:
```javascript
addItem(item): void { 
    this.todoList.push(item); 
} 
```

This will allow us to call the same function from everywhere across the application thus making our app more easy to maintain.

And now we can change our code in `app/list-manager/list-manager.component.ts` to call the `addItem` function directly from the service like so: 

```javascript
addItem(item): void { 
    this.todoListService.addItem(item); 
} 
```

- There may be additional logic when calling these methods, i.e. saving the changes in the DB (we will implement it later on)
- A better way to handle data is using immutable objects, then there will be no binding - the references will change (but we won’t implement redux in this tutorial at the moment)

