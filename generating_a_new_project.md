# Generating a new project

In every project there are few ways to start, most of the way concerning scaffolding tools like yeoman or slush.
others ways to start are using starting kit who also called seed project which contains all you need to begin the project.
unlike scaffolding tools starter kits are relevant only for the initial project and after installation you'll probably won't use that kit again (if it's a good starter kit maybe you'll back to read the doc).

regarding angular 2 the most easy way to start is the angular-cli which is a scaffolding tool and we will cover it use in this tutorial.

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
