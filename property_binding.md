# Property binding

We now have our input component, but it does not do much. We want to make it alive.

Let's make the input control text to reflect the value of our todo title variable.

This is how our input component looks now:

```javascript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'todo-input',
  template: `                           
    <input>
  `,  
  styleUrls: ['./input.component.css']  
})    
export class InputComponent implements OnInit {
  private title: string = 'My First Todo Title !!!';           

  constructor() { }                     

  ngOnInit() {
  }
}
```

When we wanted to show a variable on the page before, we used interpolation to present it.

```javascript
# code before...
template: `                           
  <input id="my-input">
  <div>{{ title }}</div>
`,  
# code after...
```

Angular then present the value of title each time that our todo input component is shown.

What if we want to show the title value inside the html input control itself ?

Using regular javascript, we can insert the value to the input via it's properties.

```javascript
let inputElement = document.getElementById('#my-input');
inputElement.value = title;
```

In javascript, we find the input element in the dom by it's id, and then set it's `value` property to the value of the title variable.

Excellent.

Angular 2 actually let us do this in the template declaration more easily and more conveniently.

```htm
<input [value]="title"
```

Behind the scene, Angular does the same thing when compiling the template and the component.

Angular looks for the `<componentName [propertyName]="variableName"` syntax and then remember to update that component property value each time the binded expression is changed.

To show this, lets change the value of the title after couple of second and see what happens.

```javascript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'todo-input',
  template: `                           
    <input [value]="title">

  `,  
  styleUrls: ['./input.component.css']  
})    
export class InputComponent implements OnInit {
  private title: string = 'My First Todo Title !!!';           

  constructor() { }                     

  ngOnInit() {
    let that = this;
    timeout(() => {
      that.title = 'This is not the title you are looking for';  
    }, 3000);
  }
}
```

The expression that we can bind to the property of the input control can be not just a variable name on our input component (property name). That expression is an Angular expression and can be a method call or any other valid Angular expression.

For example, let's bind the input value to method call that return a value.

```javascript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'todo-input',
  template: `                           
    <input [value]="titleGenerator()">

  `,  
  styleUrls: ['./input.component.css']  
})    
export class InputComponent implements OnInit {
  private title: string = 'My First Todo Title !!!';           

  constructor() { }                     

  ngOnInit() {
  }

  titleGenerator() {
      return 'This is not the title you are looking for'.
  }
}
```

So for now, we have our input control show the title of our todo in it. We now want to make the input change the value of the title back by entering value in it and pressing enter. How to do that ? Let's go to the next chapter and find out...

## Resources
[Angular Guide - Template Property Binding](https://angular.io/docs/ts/latest/guide/template-syntax.html#!#property-binding)
