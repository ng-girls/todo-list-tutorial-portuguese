# Event binding

We want our application to react to the user's actions. We want to update the title of the todo item whenever the user changes it, or to add a new item when the user presses the Save button or the Enter key.

We still don't have a whole list to show, but at the moment we will use another way to test the action. We will change it to the right functionality later on.

## The Action
First, let's implement `changeTitle`. You can replace `generateTitle` with this new method. It will receive the new title as its argument:

```ts
changeTitle(newTitle: string): void {
  this.title = newTitle;
}
```

## Binding to Events
Just like binding to element properties, we can bind to events that are emitted by the elements. Again, Angular gives us an easy way to do this. **You just wrap the name of the event with parenthesis, and pass it the method that should be executed when the event is emitted**.

Let's try a simple example, where the title is changed when the user clicks on the button. Notice the parenthesis around `click`. (We also change the binding of the input's value back to `title`.)

```html
template: `
  <input [value]="title">
  <button (click)="changeTitle('Button Clicked!')">
    Save
  </button>
  <p>The title is: {{ title }}</p>
`,
```

The event is called `click` and not `onClick` - in Angular you remove the `on` prefix from the events in the elements.

Go to the browser and see the result - click on the Save button.

## Event Data
We pass a static string to the method call: `Button Clicked!'` But we want to pass the value that the user typed in the input box!

In the next chapter we will learn how to use properties of one element in another element in the same template. Then we'll be able to complete the implementation of the click event of the Save button. 
But now we'll bind a method to an event on the input element: when the user clicks Enter, the method `changeTitle` will be called.

### 'keyup' event
When the user types, keyboard events are emitted. For example `keydown` and `keyup`. We will catch the `keyup` event \(when the pressed key is released\) and change the title:

```html
<input [value]="title" (keyup)="changeTitle('Button Clicked!')">
```

This element becomes large, so to make it easier on the eye we will split it into two lines:

```html
<input [value]="title" 
       (keyup)="changeTitle('Button Clicked!')">
```

Now when the user types in the input box, the title is changed to "Button Clicked!". But it's still a static string.

### The $event object
Now we just react when the `keyup` event occurs. Angular allows us to get the event object itself. It is passed to the event binding as `$event` - so we can use it when we call `changeTitle()`.

The event object emitted on `keyup` events has a reference to the element that emitted the event - the input element. The reference is kept in the event's property `target`. As we've seen before, the input element has a property `value` which holds the current string that's in the input box. We can pass `$event.target.value` to the method:

```html
<input [value]="title" 
       (keyup)="changeTitle($event.target.value)">
```

Check it out in the browser. Now with every key stroke, you can see the title changes and reflects the input value.

### Pressing the Enter key
You can limit the change to only a special key stroke, in our case it's the Enter key. Angular makes it really easy for us. The `keyup` event has properties which are more specific events. So just add the name of the key you'd like to listen to:

```html
<input [value]="title" 
       (keyup.enter)="changeTitle($event.target.value)">
```

Now the title will change only when the user hits the Enter key while typing in the input.

### Tip - explore the $event
You can change the changeTitle method to log the `$event` object in the console. This way you can explore it and see what properties it has. 

Change the method `changeTitle`:
```ts
changeTitle(event): void {
  console.log(event);
  this.title = event.target.value; // the original functionality still works
}
```

Now change the argument you're passing in the template:
```html
<input [value]="title" 
       (keyup.enter)="changeTitle($event)">
```

Try it out!

Don't forget to change back the code before we go on.
