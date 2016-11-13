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
    <button>
      Save
    </button>
    {{ title }}
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

We use interpolation to present to present the value of the ```title``` property: ```{{ title }}```

Angular then presents the value of ```title``` each time that our todo input component is shown.

What if we want to show the title value inside the HTML input control itself?

Every `input` element has a property called `value`, which holds the string that is displayed inside the `input` box. In HTML we can pass a string directly to the element's `value` attribute: 
```html
<input value="Hello World">
```

But we loose the dynamic binding of between the variables in the controller to the template.

Using regular JavaScript, we can insert the value to the input via its properties. We'll fetch the element from the DOM and assign the value of the member `title` to the element's `value` property.

```javascript
let inputElement = document.getElementById('#my-input');
inputElement.value = this.title;
```

In JavaScript, we find the input element in the DOM by its id, and then set it's `value` property to the value of the title variable. We need to add the id to the ```input``` element then: 
```
<input id="my-input">
```

Excellent.

However, **this is highly discouraged in Angular 2. You should never access the DOM directly!**
That's because you can assign different renderers to Angular and run the application on different platforms. They may be mobile, desktop, or even a robot. And they will not have a `document` object from which you can manipulate the result!

Angular 2 actually lets us do this in the template declaration more easily and more conveniently. We saw that with interpolation. Now we'll see how to bind to an element's property. We surround the wanted property with square brackets and pass it the class member:

```html
<input [value]="title">
```

Behind the scene, Angular does the same thing when compiling the template and the component.

Angular looks for the `<componentName [propertyName]="variableName">` syntax and then updates that component property value each time the bound expression is changed.

To show this, let's change the value of the title after a few seconds and see what happens.

```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'todo-input',
  template: `                           
    <input [value]="title">
    {{ title }}
  `,  
  styleUrls: ['./input.component.css']  
})    
export class InputComponent implements OnInit {
  private title: string = 'My First Todo Title !!!';           

  constructor() { }                     

  ngOnInit() {
    let that = this;
    setTimeout(() => {
      that.title = 'This is not the title you are looking for';  
    }, 3000);
  }
}
```

The expression that we can bind to the property of the input control can be not just a variable name on our input component (property name). That expression is an Angular expression and can be a method call or any other valid Angular expression.

For example, let's bind the input value to method call that returns a value.

```ts
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'todo-input',
  template: `                           
    <input [value]="titleGenerator()">
    {{ titleGenerator() }}
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

So for now, we have our input control show the title of our todo in it. We now want to make the input change the value of the title back by entering value in it and pressing enter. How to do that? Let's go to the next chapter and find out...

## Resources
[Angular Guide - Template Property Binding](https://angular.io/docs/ts/latest/guide/template-syntax.html#!#property-binding)
