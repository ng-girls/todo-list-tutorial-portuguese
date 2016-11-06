# The list

Now, you are going to add the todo-list itself to the component app-root. Find the root file, `src/app/app.component.ts`. Then, you need to perform two steps. First, go to `AppComponent` class, open a new line right after `private title: string = 'My Todos';` and put in the list of items for ToDo list as an array of JSON-like objects for each item. At the beginning, each item only contains a title:
```
private todoList = [
  {title: 'install NodeJS'},
  {title: 'install Angular CLI'},
  {title: 'create new app'},
  {title: 'serve app'},
  {title: 'develop app'},
  {title: 'deploy app'},
];
```

Putting info (resources) right inside your code is called hardcoding and considered an especially bad prctice. Indeed, you will move the item list to a service file later on. But let's advance step-by-step, so, defining items this way is okay for now.

Now, you have to tell the browser to display those items. For this, you will use the Angular 2 built-in directive, `*ngFOR`. It works as enhanced loop in Java. `*` is a semantic though necessary notation which causes Angular to use the current DOM element as template to render the loop.

Insert the loop right after `<todo-input></todo-input>`, this way:
```
<ul>
 +      <li *ngFor="let item of todoList">
 +        {{ item.title }}
 +      </li>
 +    </ul>
 ```
 This means "go over all items of todoList array defined below, and print out an unnumbered list which contains item titles".
