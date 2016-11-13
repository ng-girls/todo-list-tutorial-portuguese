# Generating a new project

In every project there are different ways to start, most of them concern scaffolding tools like Yeoman or Slush. These tools generate a starter project, help you generate needed files, and take care of building and running the project.
Others ways to start are using starter kits, are also called seed projects, which contain all you need to start the project.
Unlike scaffolding tools, starter kits are relevant only for the initial project. After installation you probably won't use that kit again (if it's a good starter kit maybe you'll go back to read the documentation).

Regarding Angular 2, the most easy way to start is the Angular-CLI which is a scaffolding tool.  we will cover its use in this tutorial.

In this chapter we show all the files and folders that are created by Angular-CLI when you create a new project. We'll start with one important action: changing the application prefix.

###Application prefix
The prefix is used to differentiate the components that you create in your application from components you use from other sources, and from HTML components. You can give your initials as the prefix if it's a personal project. If you're collaborating or working for a client, you can have the initials of the project name as the prefix. In this tutorial, the prefix will simply be `todo`. 

Angular-CLI generated a configuration file for its own use: `angular-cli.json`. Open this file, find the `prefix` property and change its value from `app` to `todo`. From now on, each component and directive you will create using Angular-CLI will have this prefix in its selector.

We could have defined the prefix when we created the project, by adding `--prefix <prefix>`. Then even the root component that is generated would have this prefix. But we're fine with its current selector, `app-root`, and we will not change it at this moment.

###Application structure

the first thing to start with when you work with the cli is scaffold the initial project.
to do so you can simply create a folder and write `ng init`
from that point angular-cli will download all the dependencies and install them.
other way to scaffold the initial project is writing `ng new <project-name>` and angular-cli will create the folder for you and `ng init` in that folder.

after we created the project we will get file in this format
```
├── angular-cli.json // angular cli configuration
├── e2e // end to end testing
├── karma.conf.js // testing configuration file
├── package.json // package configuration file
├── protractor.conf.js // testing configuration file
├── README.md // your readme
├── src // your code in here
│   ├── app
│   │   ├── app.component.css
│   │   ├── app.component.html
│   │   ├── app.component.spec.ts
│   │   ├── app.component.ts
│   │   ├── app.module.ts
│   │   └── index.ts
│   ├── assets // pictures etc
│   ├── environments // environments variables
│   │   ├── environment.prod.ts
│   │   └── environment.ts
│   ├── favicon.ico // the browser icon
│   ├── index.html
│   ├── main.ts
│   ├── polyfills.ts
│   ├── styles.css
│   ├── test.ts
│   ├── tsconfig.json // typescript configuration
│   └── typings.d.ts
└── tslint.json // linting configuration
```

lets skip all the configurations files for now and jump right to the folder structure.
the app is the main component of the application from that point we start our app.
we will cover components in more depth in later tutorial but the main idea of the project is that we create a components and connect them to each other until we have an application.

with angular-cli we can generate components and some other files which can help us in the future.
to do so we should write `ng generate component <component name>` for components and `ng generate route <route path>` for routes and may more which can be review in [angular cli docs](https://github.com/angular/angular-cli#generating-components-directives-pipes-and-services)

now you probably ask how do you see and review your application?
your command for that would be `ng serve` and you'll be able to access you app in `http://localhost:4200`
and last but not least if you want to build your application for production you should write `ng build` and there you have it, easy way to scaffold you angular 2 application
