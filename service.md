# Service

What and why
------------
Services are JavaScript functions that are responsible for doing a specific task only. Angular services are injected using Dependency Injection mechanism and include the value, function or feature which is required by the application. In our ToDo app, we will need a service to save all the tasks and to use it by injecting it into the components.

Create
------------
In order to create a new service by **angular-cli**, we need to type this command on the root folder:

    ng g s todoList

This command will generate the service and put it under src/app/todo-list.service.ts

Provide in ngModule 
------------
Now, to start using the service, we first need to provide it in the @NgModule component.
In /src/app/app.module.ts , add an import code:
```javascript
import { TodoListService } from './todo-list.service';
````
And now add the service to the "providers" array, that the ngModule component will look like this:
```javascript
@NgModule({
  declarations: [
    AppComponent,
    InputComponent,
    ItemComponent,
    ListManagerComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpModule
  ],
  providers: [TodoListService],
  bootstrap: [AppComponent]
})
````

That will allow us to create the service instance and to use it in any place of our app.

Move list from component to service
------------
We now need to move the todoList array from the component to our new service. The service will now have:
```javascript
private todoList = [
    { title: 'install NodeJS' },
    { title: 'install Angular CLI' },
    { title: 'create new app' },
    { title: 'serve app' },
    { title: 'develop app' },
    { title: 'deploy app' },
  ];
```

Create method on service to return the list
------------
Now go to the generated service file, found in src/app/todo-list.service.ts , and add a "getTodoList" function that will return the todoList array. The service will look like this:
```javascript
import { Injectable } from '@angular/core';

@Injectable()
export class TodoListService {

  private todoList = [
    { title: 'install NodeJS' },
    { title: 'install Angular CLI' },
    { title: 'create new app' },
    { title: 'serve app' },
    { title: 'develop app' },
    { title: 'deploy app' },
  ];

  constructor() {
  }

  getTodoList() {
    return this.todoList;
  }
}
```

Inject to list-manager component and use the service 
------------
After creating the service instance, we can inject it to our list-manager component. Go to /src/app/list-manager/list-manager.component.ts file and add the folllowing import code:
```javascript
import { TodoListService } from '../todo-list.service'; 
````

And just use it in ListManagerComponent class: Remove the todoList array but keep the todoList member and change the constructor to be:
```javascript
constructor(private todoListService:TodoListService) { }
```

And now the todoList will use the service we created on **ngOnInit** function:

```javascript
ngOnInit() {
    this.todoList = this.todoListService.getTodoList();
}
```

