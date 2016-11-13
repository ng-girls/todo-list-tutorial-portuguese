# New component todo-item

We will create a new component which will be used for each todo item that is displayed on the list. It will be a simple component at first, but it will grow later on. What's important is that it will get the todo item as an input from its parent component.

Create a new component called `item`: 

```
ng g c item -it
```

You can see a new folder was created with the component files inside. 

Use the component in the `app-root` - inside the `<li>` element:

```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item></todo-item>
  </li>
</ul>
```

Check out the result in the browser. What do you see? Why?

We want to display the title of each item from within the `todo-item` component. We need to pass the title of the current item in the loop (or the whole item) to the `todo-item` component. 

Again, Angular makes it really easy for us, by providing us the `Input` decorator.

In the `todo-item` component class (itemComponent) add the line:
```ts
@Input() itemTitle: string;
```
It tells the component to expect an input of type string and to assign it to the class property called `itemTitle`. Make sure that `Input` is added to the import statement in the first line in the file. Now we can use it inside the `todo-item` template:
```html
{{ itemTitle }}
```

You can add any other HTML elements you'd like here. 

Now we need to pass a string, which is the item's title, where we use the component. Go back to the `app-root` component and add pass the item title:
```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item [itemTitle]="item.title"></todo-item>
  </li>
</ul>
```

We use property binding on an element we created ourselves! And now we can actually see and understand that property binding binds to actual proberty of the component. 

We will refactor our code a bit so we can easily implement more functionality in the `todo-item` component, for example editing and removing the item. Instead of passing just the title to the component, we will pass the whole item, and let the component extract the title where needed.

In the `todo-item` component change the interpolation in the template to:
```html
{{ todoItem.title }}
```
Rename the Input member and change its type: 
```ts
@Input() todoItem: any;
```

Now pass the whole item to the renamed property in `app-root`:
```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item [todoItem]="item"></todo-item>
  </li>
</ul>
```


