# \#15:  🔋 Creating a Service

In Angular, a service is \(typically\) a JavaScript class that's responsible for performing a specific task needed by your application. In our todo-list application, we'll create a service that will be responsible for saving and managing all the tasks, and we'll use it by injecting it into the components.

## Create a service with the Angular CLI:

```text
ng g s services/todo-list
```

This command will generate the service in the file `src/app/services/todo-list.service.ts`. The service is a simple Class called `TodoListService`. It has the decorator `@Injectable` which allows it to use Dependency Injection.

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```text
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class TodoListService {

  constructor() { }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Provide the service

In version 6 of the Angular CLI you don't need to provide the service by yourself - the CLI adds it to the root `NgModule`. But you can keep on reading to understand what happens and what it means.

To start using the service, we first need to _provide_ it in an `NgModule`. We have only one `NgModule` in our app - the `AppModule` located in `/src/app/app.module.ts`. It's an empty class preceded by the `@NgModule` decorator to which we pass a configuration object. One of the properties of this object is a `providers` list which is currently empty. We'll add our new service to the list. 

{% code-tabs %}
{% code-tabs-item title="src/app/app.module.ts" %}
```typescript
@NgModule({
  declarations: [
    AppComponent,
    InputButtonUnitComponent,
    TodoItemComponent,
    ListManagerComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [TodoListService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The `providers` array tells Angular how to provide a service we're looking for \(usually in a component or another service\). This time the recipe is simple: When we ask for the `TodoListComponent` class we expect to get an instance of this class. Angular will create only one instance that we can access from anywhere in our application \(a Singleton\), so we can use it to share data between different parts of the application.

Make sure that the service is imported:

{% code-tabs %}
{% code-tabs-item title="src/app/app.module.ts" %}
```typescript
import { TodoListService } from './services/todo-list.service';
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Share data

Now we can move the `todoList` array from `ListManagerComponent` to our new service. Go to the generated service file, `src/app/services/todo-list.service.ts`, and add this code inside the `TodoListService` class just above the `constructor`:

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
private todoList: TodoItem[] = [  {title: 'install NodeJS'},
  {title: 'install Angular CLI'},
  {title: 'create new app'},
  {title: 'serve app'},
  {title: 'develop app'},
  {title: 'deploy app'},
];
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Make sure that the TodoItem interface is imported:

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
import { TodoItem } from '../interfaces/todo-item';
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Create a method to return the list

We'll add a `getTodoList` method that will return the `todoList` array. The service will look like this:

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
import { Injectable } from '@angular/core';
import { TodoItem } from '../interfaces/todo-item';

@Injectable({
  providedIn: 'root'
})
export class TodoListService {

  private todoList: TodoItem[] = [
    {title: 'install NodeJS'},
    {title: 'install Angular CLI'},
    {title: 'create new app'},
    {title: 'serve app'},
    {title: 'develop app'},
    {title: 'deploy app'},
  ];

  constructor() { }

  getTodoList() {
    return this.todoList;
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Inject and use the service

After creating the service, we can inject it into our `list-manager` component. In Angular Dependency Injection is very simple. We pass it as a parameter in the constructor - the parameter's type is the class name of the service. Angular assigns the instance it created to the parameter name, and we can use it from within the constructor. Before implementing it ourselves, let's see how it works:

```typescript
constructor(todoListService: TodoListService) {
  todoListService.getTodoList();
}
```

Typescript helps us furthermore by giving a shortcut for assigning the parameter to a class member. By adding `private` or `public` before the parameter name it is automatically assigned to `this`. So instead of declaring and assigning the property by ourselves: 

```typescript
export class ListManagerComponent implements OnInit {
  todoListService: TodoListService;
  
  constructor(todoListService:TodoListService) { 
    this.todoListService = todoListService;
  }
}
```

...we can reduce a lot of code like this:

```typescript
export class ListManagerComponent implements OnInit {
  
  constructor(private todoListService:TodoListService) { }
}
```

So let's go on and use the service in the `list-manager` component.

* Remove the hard-coded list from the component, keep only the `todoList` property declaration.
* Inject the `TodoListService` using the constructor. 

```typescript
export class ListManagerComponent implements OnInit {
  todoList: TodoItem[];
  
  constructor(private todoListService:TodoListService) { }
```

* Make sure the `TodoListService` is imported.

{% code-tabs %}
{% code-tabs-item title="src/app/list-manager/list-manager.component.ts" %}
```typescript
import { TodoListService } from '../services/todo-list.service';
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Get the list from the service in the `ngOnInit` method.

{% code-tabs %}
{% code-tabs-item title="src/app/list-manager/list-manager.component.ts" %}
```typescript
ngOnInit() {
  this.todoList = this.todoListService.getTodoList();
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

You don't need to change anything in the template since we're assigning the list to the same property we used before. Seems like nothing has changed, but you can check that the list comes from the service by changing it from there \(adding an item, changing a title, etc.\).

