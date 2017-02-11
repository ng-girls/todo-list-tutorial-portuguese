# New component todo-item

We will create a new component which will be used for each todo item that is displayed on the list. It will be a simple component at first, but it will grow later on. What's important is that **it will get the todo item as an input from its parent component**. This way it can be a reusable component, and not rely directly on the application's data and state.

Create a new component called `item`: 

```
ng g c item -it
```

You can see a new folder was created with the component files inside. 

Use the component in the template of `appComponent` - inside the `<li>` element:

```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item></todo-item>
  </li>
</ul>
```

Check out the result in the browser. What do you see? Why?

## @Input()
We want to display the title of each item from within the `todo-item` component. We need to pass the title of the current item in the loop (or the whole item) to the `todo-item` component. 

Again, Angular makes it really easy for us, by providing us the `Input` decorator.

Inside the newly generated `itemComponent` class (itemComponent) add the line:
```ts
@Input() itemTitle: string;
```
It tells the component to expect an input of type string and to assign it to the class member called `itemTitle`. Make sure that `Input` is added to the import statement in the first line in the file. Now we can use it inside the `itemComponent` template:
```html
{{ itemTitle }}
```

You can add any other HTML elements you'd like here. 

Now we need to pass a string, which is the item's title, where we use the component. Go back to `appComponent` and  pass the item title to the `todo-item`:
```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item [itemTitle]="item.title"></todo-item>
  </li>
</ul>
```

The `itemTitle` here in square brackets is the same as declared as the component's `@Input`.

We use property binding on an element we created ourselves! And now we can actually see and understand that property binding binds to actual property of the component. 

## Passing the whole item
We will refactor our code a bit so we can easily implement more functionality in the `todo-item` component, for example editing and removing the item. Instead of passing just the title to the component, we will pass the whole item, and let the component extract the title where needed.

In `itemComponent` change the interpolation in the template to:
```html
{{ todoItem.title }}
```
Rename the Input member and change its type: 
```ts
@Input() todoItem: any;
```

Now pass the whole item to the renamed property in `appComponent` (remove the `.title`):
```html
<ul>
  <li *ngFor="let item of todoList">
    <todo-item [todoItem]="item"></todo-item>
  </li>
</ul>
```

We now have a list of components, so each component received its data from the loop in the parent component. Now we'll see how this list can be dynamic.
