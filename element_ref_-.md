# Element ref

In the last chapter, we ended with our input component that can reflect and change the value of title of our todo item. `input.component.ts` should look like this:

```javascript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'todo-input',
  template: `                           
    <input [value]="title"              
           (keyup.enter)="changeTitle($event.target.value)">
    <button (click)="changeTitle('Button Clicked!')">
      Save
    </button>
    <p>The title is: {{ title }}</p>
  `,  
  styleUrls: ['./input.component.css']  
})    
export class InputComponent implements OnInit {
  private title: string = '';           

  constructor() { }                     

  ngOnInit() {
  }

  changeTitle(newTitle: string): void {
    this.title = newTitle;              
  }
}
```

Now, we want to take the value of the input (that the user typed) and change the title when we press the Save button.

We already know how to create a button and react to click on it. We now need to pass to the method some data from a different element. We want to use the input's value from inside the button element.

Angular helps us do exactly that. **We can get a reference to the element we want into a variable with the name we choose, **for example** `inputElement`, using a simple syntax - a hash.** Add `#inputElement` to the `input` element, and use it in the click event of the button:

```html
<input [value]="title"              
       (keyup.enter)="changeTitle($event.target.value)"
       #inputElement>

<button (click)="changeTitle(inputElement.value)">
  Save
</button>
```

Now we can use the value that the user entered in the input element in the method called when clicking the Save button!

What is that `#` we see ?

Angular lets us define a new local variable named `inputElement` \(or any name you choose\) that holds a reference to the element we defined it on, and then use it any way we want. In our case, to access the value property of the input.

Instead of hunting down the elements via DOM query \(which is bad practice as we discussed\), we now can put element references in the template and access each element we want declaratively.

Next on, we'll build the list of todo items.

### Tip - explore the element reference
Just like we did in the previous chapter, when we logged $event, you can do the same with `#inputElement`. Change the method `changeTitle` so it will receive the whole element reference and log it to the console:

```html
<button (click)="changeTitle(inputElement)">
```
```ts
changeTitle(inputElementReference): void {
  console.log(inputElementReference);
  this.title = inputElementReference.value;              
}

```

## Resources

[Angular Template Reference Variables](https://angular.io/docs/ts/latest/guide/template-syntax.html#!#ref-vars)

