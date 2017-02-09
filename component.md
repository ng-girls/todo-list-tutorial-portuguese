# Component

One approach in Web development \(and software development generally\) is component-based architecture. In the past years it gains a lot of popularity. What is a component?

Helmut Petritsch defines in [Service-Oriented Architecture \(SOA\) vs. Component Based Architecture](http://petritsch.co.at/download/SOA_vs_component_based.pdf):

> A component is a software object, meant to interact with other components, encapsulating certain functionality or a set of functionalities. A component has a clearly defined interface and conforms to a prescribed behaviour common to all components within an architecture.

In Web applications, **a component controls a patch of screen called a view**. It's a part of what you will eventually see on the screen. It has a template, which defines its visual structure. It also has logic which defines the behavior and the dynamic values. The logic part is JavaScript code and is called the controller.

Here's a diagram of a component in Angular, with the result below.  
![Angular 2 Component](Angular Component.001.jpeg)

Directives, pipes and services are other building blocks in Angular, which we will discuss later in the tutorial.

Let's take a look at the component that was created by Angular-CLI. All the relevant files exist in the folder `src/app`. Open the file `app.component.ts`.

Just like ngModules that we saw in the previous chapter, a component is also defined by a class with a decorator. This is the class definition:

```js
export class AppComponent {
  title = 'todo works!';
}
```

It has one member called "title". It is a variable to which you can assign a value. The value assigned to it here is the string "todo works!".

Angular takes care of synchronizing the members of the component with the component template. So we can easily use the member `title` in the template. Take a look at the file `app.component.html` - this is the template attached to the component:

```html
<h1>
  {{ title }}
</h1>
```

The double curly braces and their content are called **Interpolation**. This is one form of ** data binding** in Angular. As we mentioned before, the code in this file is not used as is when the browser renders the component. Angular compiles it to JavaScript code. In one of the compilation steps it looks for Interpolations inside the template. **The content of the Interpolation is an expression, written in JavaScript.** In run time the expression is evaluated, and then you see the result.

Interpolation is one of the strongest, most basic features in Angular. It exists from the very beginning of Angular - in the first version. It makes it really simple to insert dynamic data into the view.

In this component, the expression is simply the member of the component class, `title`. **Let's try to change it**. Try out the following and see the result in the browser. \(With every change you make in the file, the browser will refresh automatically!\)

* Remove the curly braces and keep just the content `title`
* Put back the curly braces and replace the content with some mathematical expression, for example: `{% raw %}{{ 2 + 2 }}{% endraw %}`. \(The spaces are not mandatory, they just make the code more readable.\)
* Write a mathematical expression combined with the `title` member: `{% raw %}{{ title + 10 }}{% endraw %}`
* Pass an undefined variable to the expression - a variable which was not declared in the component class. For example: `{% raw %}{{ x }}{% endraw %}`
* Try out anything you'd like. Don't worry - you can't do any harm to the browser or the computer! In the worst case, the browser will run out of memory and will get stuck. \(But you'll have to write something really complicated to make that happen!\)

This is one way that you can bind members of the component's controller to its template. How does Angular know that this is the template of the App component?

Let's go back to the file `app.component.ts` and look at the component's meta-data defined in the decorator `@Component` right above the class definition:

```js
@Component({
  selector: 'todo-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
```

We pass an object of definitions to the decorator, just like we saw in the previous chapter with ngModule. The second property, `templateUrl` tells Angular where to look for the template attached to the component. There is another option to point to the template, which is better practice: to write the whole template inline here, in the component definition. We will discuss it later.

The third property, `styleUrls` tells Angular where to look for the CSS files that define the style of this component. It can have multiple CSS files. That's why the value of `styleUrls` is an array. You can take a look at the CSS file `app.component.css` - you'll see that it's empty. You can add some CSS style here, for example:

```css
h1 {
  color: red;
}
```

We'll add more style later on.

The first property, `selector`, tells Angular what will be the name of the tag that we'll use to call the component. As we saw in the file `src/index.html`, we use the app component inside the body:

```html
<body>
  <todo-root>Loading...</todo-root>
</body>
```

The element `todo-root` is not an HTML element. It is the component that was created with the selector `todo-root`. Try changing the selector. You'll see that if you change it in only one of the files, "Loading..." will be displayed. This is the content that we gave to the tag in `index.html`, and it is rendered as long as the element is not replaced with an Angular component. You can see in the browser's console an error message.

One last thing, the first line in the component file imports the code that defines the decorator `@Component`. It is needed to use the decorator, which is defined in the imported file \(or actually, in one of its own imports\). Try removing this line, and see the error.

### Best Practice

Let's add some best practice to the component.

#### Inline Template
First, lets move the template to be **inline** in the component definition. Replace the line

```js
templateUrl: './app.component.html',
```

with

```js
template: ``,
```

Notice the **backticks** - they are used to define Template Literals, which are new in JavaSript \(ES6\). This way you can define multi-line strings. They have another cool ability: to easily use JavaScript variables and expressions within the string \(with no relation to Angular binding expressions in the template\). Read about it in the [MDN documentation](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Template_literals).

Make sure you replace `templateUrl` with `template` and don't forget the comma in the end of the line.

Now copy the entire template from `app.component.html` and paste it between the backticks.  We'll reformat the code a bit to have it easier on the eye:

```js
template: `
  <h1>
    {{ title }}
  </h1>  
`,
```

It is easier to manage the template when you see its controller at the same time. This is true as long as the template doesn't get too long and the controller doesn't get too complicated. If they do, it's a sign you should refactor your code by breaking it down to child components.

At this point you can delete the file `app.component.html`.

The same way we use inline template, we can use also inline styles. But for now we will keep the styles in a separate file.

####Variable Types
Another best practice we are going to add is using TypeScript's ability to define the **type** of the class member `title`. It is best to define types anywhere possible, because it can help you avoid mistakes and bugs. It also allows the IDE to help you when using variables and functions. The IDE can tell you what type of value is expected, and suggest completions.

First, we'll define `title` to be a private member. It will prevent trying to access `title` from code outside this class. \(The template is a part of the class.\) Add `private` before `title`.

Second, we'll define that `title`should receive only values of type `string.` Add `: string`after `title`. This way we'll get an error if we try to assign something else. Available types are **string, boolean, number, any** \(if you want to allow any type\) and **custom types** defined by classes and interfaces. For example, `AppComponent` is an available type.

The line defining the `title` member should now look like this:

```ts
private title: string = 'app works!';
```

You can try assigning something else to the title now, for example a number. See how the IDE tells you that something is wrong.

We have explored the root component that was generated for us by Angular-CLI, and even refactored it. In the next chapter we will create a new component. We will start building the tree of components, which defines the structure of the application.

