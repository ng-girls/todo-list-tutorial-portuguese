# Gerando um novo projeto

Em todos os projetos há formas diferentes de começar, a maioria deles se refere a ferramentas de scaffolding como Yeoman ou Slush. Essas ferramentas geram um projeto inicial e ajudam você a gerar os arquivos necessários e cuidar da construção e execução do projeto.

Outras formas de começar estão usando kits de inicialização, também são chamados de projetos de semente, que contêm tudo o que você precisa para iniciar o projeto.

Ao contrário das ferramentas de scaffolding, os kits de inicialização são relevantes apenas para o projeto inicial. Após a instalação, você provavelmente não usará esse kit novamente \(se for um bom kit de inicialização, talvez você volte a ler a documentação\).

Em relação ao Angular, a maneira mais fácil de começar é o Angular-CLI, que é uma ferramenta de scaffolding. Vamos abordar o seu uso neste tutorial.

Neste capítulo, mostramos todos os arquivos e pastas criados pelo Angular-CLI quando você cria um novo projeto. Começaremos com uma ação importante: alterando o prefixo do aplicativo.

### Prefixo de aplicação

The prefix is used to differentiate the components that you create in your application from components you use from other sources, and from HTML components. You can give your initials as the prefix if it's a personal project. If you're collaborating or working for a client, you can have the initials of the project name as the prefix. In this tutorial, the prefix will simply be `todo`.

Angular-CLI generated a configuration file for its own use: `angular-cli.json`. Open this file, find the `prefix` property and change its value from `app` to `todo`. From now on, each component and directive you will create using Angular-CLI will have this prefix in its selector.

We could have defined the prefix when we created the project, by adding `--prefix <prefix>`. Then even the root component that is generated would have this prefix. But we're fine with its current selector, `app-root`, and we will not change it at this moment.

### Estrutura da Aplicação

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
│   ├── app
│   │   ├── app.component.css
│   │   ├── app.component.html
│   │   ├── app.component.spec.ts
│   │   ├── app.component.ts
│   │   ├── app.module.ts
│   │   └── index.ts
│   ├── assets // pictures etc
│   ├── environments // environments variables
│   │   ├── environment.prod.ts
│   │   └── environment.ts
│   ├── favicon.ico // the browser icon
│   ├── index.html
│   ├── main.ts
│   ├── polyfills.ts
│   ├── styles.css
│   ├── test.ts
│   ├── tsconfig.json // typescript configuration
│   └── typings.d.ts
└── tslint.json // linting configuration
```

lets skip all the configurations files for now and jump right to the folder structure.  
the app is the main component of the application from that point we start our app.  
we will cover components in more depth in later tutorial but the main idea of the project is that we create a components and connect them to each other until we have an application.

with angular-cli we can generate components and some other files which can help us in the future.  
to do so we should write `ng generate component <component name>` for components and `ng generate route <route path>` for routes and many more which can be review in [angular cli docs](https://github.com/angular/angular-cli#generating-components-directives-pipes-and-services)

now you probably ask how do you see and review your application?  
your command for that would be `ng serve` and you'll be able to access you app in `http://localhost:4200`  
and last but not least if you want to build your application for production you should write `ng build` and there you have it, easy way to scaffold you Angular application

