# Class


##class definition 
Class is a special programmatic structure. It is defined with **members** which can be  **properties** (variables) and **methods** (functions). Then instances of the class are created, usually by calling the ```new``` operator on the class: ```let myInstance = new myClass();```. The instance created is an object on which you can call the class methods and get and set its properties' values. Multiple copies can be created from one class. 

###in Angular...
Angular takes care of creating instances of the classes you define - if they are recognized as Angular building blocks. The decorators make that connection with Angular. 

Each time you use a component in a template, a new instance of it is created. For example, here three instances of the inputComponent class will be created: 
```html
template: `
  <todo-input></todo-input>
  <todo-input></todo-input>
  <todo-input></todo-input>
`
```

Let's take a look at the class ```inputComponent```.

###implements OnInit

First, you see something was added to the class declaration: 
```ts
export class InputComponent implements OnInit {
  ...
}
```

OnInit is an interface - a structure defined but not implemented as a class. It defines which properties and/or methods should exist on a class that implements it. In this case, OnInit is an interface for Angular Components which implement the method ```ngOnInit```. This method is a component life-cycle method. Angular will call this method after the instance is created. 

Angular-CLI adds this statement to remind us that it's best to initialize things on the component through the ```ngOnInit``` method. You can see it also added the method in the body of the class:

```ts
ngOnInit() {
}
```

You can use this method without explicitly indicating that the class implements the OnInit interface. But it's useful to use the implementation statement. To see how, delete the ```ngOnInit``` method. The IDE will tell you there's an error - you must implement ```ngOnInit```. How does it know that? Because of ```implementing OnInit```.

###constructor

Another method we haven't seen in the ```app-root``` component is the constructor. It is a method that is called by JavaScript when an instance of the class is created. Whatever is inside this method is used to create the instance. So it is called before ```ngOnInit```.

###properties
The property ```title``` we added is used to store a value, in our case of type string. Each instance of the class will have a different ```title```, meaning you can change the value of ```title``` in one instance, but it will remain the same in the other instances. 

In TypeScript we must declare members of the class either in the class body outside any method, or pass it to the constructor - as we will see when we will use a service. 

You can declare the property without initializing it:
```ts
private title: string;
```
Then you can assign a value at a later stage, for example in the constructor or in the ngOnInit method. When referencing a member of the class from within a class method you must prefix it with ```this```. It's a special property that points at the current instance. 

Try setting a different value for ```title``` from inside the constructor. See the result in the browser:

```ts
private title: string = 'my title';

constructor() { 
  this.title = 'Hello World';
}
```

Try changing the value of ```title``` inside the method ```ngOnInit```. Which value will be displayed on the screen?

###methods

Let's add a method that changes the value of ```title``` according to the argument we will pass. The method will have one parameter of type string. Add inside the class body (but not inside another method):

```ts
changeTitle(newTitle:string): void {
  this.title = newTitle;
}
```

The method is called ```changeTitle```. It doesn't have a return statement, so we noted that it "returns void". We can change that if we return an actual value. For example: 

```ts
changeTitle(newTitle:string): string {
  this.title = newTitle;
  return this.title;
}
```

This method is not used anywhere. We can call it from another method or from the template (which we will see in the following chapters). Let's call it from the constructor.

```ts
constructor() { 
  this.changeTitle('I love Angular');
}
```

You can try calling the method with different arguments (the string passed inside the brackets) from ngOnInit. Try calling it before or after assigning a value directly to ```title```. Try calling it a few times from the same method. See the result in the browser. 

###debugging tip
You can always use ```console.log(someValue)``` inside class methods. Then the value you passed as an argument will be printed in the browser's console. This way you can see the order of the execution of the methods and the value of the argument you pass (if it's a variable). For example: 

```ts
constructor() { 
  console.log('in constructor');
  this.changeTitle('I love Angular');
  console.log(this.title);
}
```


