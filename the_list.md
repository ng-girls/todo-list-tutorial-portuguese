# The list

Now, you are going to add the todo-list itself to the component `app-root`. Open the file `src/app/app.component.ts`. Add the list of items inside the `AppComponent` class as an array of objects for each item. At this stage each item will contains only a title:

```js
private todoList = [
  {title: 'install NodeJS'},
  {title: 'install Angular CLI'},
  {title: 'create new app'},
  {title: 'serve app'},
  {title: 'develop app'},
  {title: 'deploy app'},
];
```

> Putting info \(resources\) right inside your code is called hardcoding and considered an especially bad practice. Eventually we'll get the list from an outer resource, but even if not it's best to mock data in their own files. But let's advance step-by-step, so defining items this way is okay for now.

Now, you have to tell the browser to display those items. For this, you will use the **Angular built-in directive, `*ngFor`**. It works as an enhanced loop in Java. `*` is a semantic though necessary notation which causes Angular to use the current element as template when rendering the list.

Insert the loop right after `<todo-input></todo-input>`, this way:

```html
<todo-input></todo-input>
<ul>
  <li *ngFor="let item of todoList">
    {{ item.title }}
  </li>
</ul>
```

This means "go over all items of todoList array defined below, and print out an unnumbered list which contains the items' titles". While looping over the `todoList`, each item is assigned to the variable `item`, and we can use this variable inside the `li` element and its children.

### Angular directives

Directives are pieces of logic \(written as classes\) that can be attached to elements and components. They are used to change the display or the behavior of the element. Angular comes with some built-in directives.

As we saw, the `ngFor` directive modifies the template in run-time by repeating the element it's called on and its content. Another directive, for example, is `ngIf`, which receives a Boolean expression. Only if the expression is true Angular renders the element and its content. It also needs the `*` prefix because it uses the target element as a template, similarly to the `*ngFor` directive. For example:

```html
<h1 *ngIf="userLoggedIn">Welcome!</h1>
```

In this example, `userLoggedIn` should be a member of the component, and have a true or false value. If it's true, the element will be displayed. If false, the element will not exist on the DOM.

There are other directives in Angular which are not structural \(and are used without the `*`\). For example ngStyle and ngClass, with which you can dynamically apply style and classes to the element.
