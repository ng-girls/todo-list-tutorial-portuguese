# A new component

In this chapter we will write a whole new component. It will allow us adding an item to the todo list. It will be composed of the HTML elements `input` and `button`.

We'll use Angular-CLI to generate all the needed files and boilerplate for us. In the terminal run:

```cmd
ng g c input -it
```

As we've seen before, `ng` is the command for using Angular-CLI. `g` is a shorthand for `generate`. `c` is a shorthand for `component`. `input` is the name we give to the component. `-it` is shorthand for `--inline-template`.

So the long version of the command is:

```
ng generate component input --inline-template
```

> You can avoid using `-it` each time you generate a components by setting inline templates as a default in the configuration file `angular-cli.json`.
>
> Don't worry about the component name `input`. It will not replace HTMLs `input` element. That's thanks to the prefix that Angular-CLI gives to our components. The default prefix is `app`, so the component selector would be `app-input`. If you've created the project stating the prefix of your choice, or changed it afterwards in the file `angular-cli.json`, this will be the prefix of the selector. When we created the project we set the prefix to "todo", so the selector should be `todo-input`.

Let's take a look of what Angular-CLI created for us.

It created a new folder called `src/app/input`. There are three files there:

* `input.component.css` - this is where the style that's specific to the component will be placed.
* `input.component.spec.ts` - this is a file for testing the component. We will not deal with it on this tutorial.
* `input.component.ts` - this is the component file where we will define its template and logic.

Open the file `input.component.ts`. You can see that Angular-CLI has generated a default template for us:

```js
template: `
    <p>
      input Works!
    </p>
  `,
```

It has also added the selector according to the name we gave to the component, with the prefix we configured:

```js
selector: 'todo-input',
```

We can use this component as is and see the result!

Open the root component file, `app.component.ts` and add the todo-input tag anywhere inside the template:

```js
template: `
  <h1>
    {{title}}
  </h1>

  <todo-input></todo-input>
`,
```

Check what's new in the browser!

Get back to our `input.component.ts` and add some content. First, add a `title` member which we will use as the todo item title:

```ts
export class InputComponent implements OnInit {
  title: string = '';
  ...
```

It will not interfere with the `todo-root` component's `title`, since each component's content is encapsulated within it.

You can give an initial string to the title, like we did in the `todo-root` component.

Next, add an input element, a button, and a binding to the title, to the template:

```html
<input>
<button>Save</button>
<p>The title is: {{ title }}</p>
```

Check out the result!

This component doesn't do much at this point. In the next chapters we will learn about the component class, and then implement the component's logic.

