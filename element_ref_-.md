# Element ref - #

In the last chapter, we ended with our beautiful input component that can reflect and change the value of title of our todo item.

```javascript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'todo-input',
  template: `                           
    <input [value]="title"              
           (keyup.enter)="changeTitle($event.target.value)">

    {{ title }}
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

Now, we want to take the value of the input and save it to our currently imaginary database when we press a button.

How do we do that?

We already now how to create a button and react to click on it.

```html
<input [value]="title"              
       (keyup.enter)="changeTitle($event.target.value)"
       id="my-beautiful-input">

<button (click)="changeTitle()">
  Save
</button>
```

```javascript
changeTitle(newTitle: string): void {
    this.title = newTitle;              
}
```

But wait, the change method expect that we pass it the value of the new title. How does we pass the input value to the function from the template ?

Let go back a little and see how would we do that in the function itself without the parameter.

```javascript
changeTitle(): void {
  let inputElement = document.getElementById('my-beautiful-input');

  this.title = inputElement.value;              
}
```

Angular, in the Template world, helps us do exactly that and access and get the element we want into a variable like `inputElement` by a simple syntax.

```htm
<input [value]="title"              
       (keyup.enter)="changeTitle($event.target.value)"
       #myInput>

<button (click)="changeTitle(myInput.value)">
  Save
</button>
```

What is that `#` we see ?

Angular let's use define a new local variable named `myInput` that hold the dom element we defined it on, and then use it any way we want. In our case, to access the value property of the input.

Instead of hunting down the elements via dom query, we now can put element references in the template and access each element we want declaratively.

On to the next chapter...

## Resources
[Angular Template Reference Variables](https://angular.io/docs/ts/latest/guide/template-syntax.html#!#ref-vars)
