#Adding A Checkbox

We are now able to interact with our todo list by removing items. But what if we want to complete items and still be able to see them on our list, for example, have a line-strike through the todo title? Enter the checkbox!

We will look at:

* Adding a checkbox
* Adding functionality when you click the checkbox so that a CSS class, which adds a strike-through style, is added to our todo items
* Edit the todo title so that it will respond to the checkbox
* Adding a new CSS Class

Let's go ahead and add a checkbox into our item.component.ts file. Place the following code right before the `<p>` tag containing `{{ todoItem.title}}`:

```html
  <input type="checkbox"/>
```
Now, in order for the checkbox to do anything we need to add a click event which we will call completeItem(). Let's do that now:

```html
  <input type="checkbox" (click)="completeItem()"/>
```
When we click on the checkbox it will run the completeItem() function. Let's talk about what this function needs to accomplish. We want to be able to toggle some CSS styling on the todo title so that when the checkbox is checked it will have a line-strike through it, and no line-strike when unchecked. In order to achieve this we will toggle a variable to be either true or false to represent checked or unchecked states. Add the following code to the ItemComponent class:

```js
private isComplete: boolean = false;

completeItem() {
  this.isComplete = !this.isComplete;
}
```

But wait! How is any of this going to affect the todo title when we're only touching the checkbox??? Well, Angular2 has this wonderful directive called NgClass. This directive applies or removes a class based on a boolean value (true or false). There are many ways to use this directive(see documentation: https://angular.io/docs/ts/latest/api/common/index/NgClass-directive.html) but we will focus on using it like so:

```html
<some-element [ngClass]="{'first': true, 'second': true, 'third': false}">...</some-element>
```

The 'first' and 'second' class will be applied to the element because they are given a true value, whereas, the 'third' class will not be applied because it is given a false value. So this is where our earlier code comes into play. Our completeItem() function will toggle between true and false values, thus dictating whether a class should be applied or removed.

Let's add this NgClass directive to our todo title now:

```html
<p class="todo-title" [ngClass]="{'todo-complete': isComplete}">
  {{ todoItem.title }}
</p>
```

And finally, add the css to our item.component.css file

```css
  .todo-complete {
    text-decoration: line-through;
  }
```

Voila! Checking the checkbox should apply a line through the todo title, and unchecking the checkbox should remove the line.
