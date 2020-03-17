# Apêndice 1: Gerando um novo projeto

Em todos os projetos há formas diferentes de começar, a maioria deles se refere a ferramentas de scaffolding como Yeoman ou Slush. Essas ferramentas geram um projeto inicial e ajudam você a gerar os arquivos necessários e cuidar da construção e execução do projeto.

Outras formas de começar estão usando kits de inicialização, também são chamados de projetos de semente, que contêm tudo o que você precisa para iniciar o projeto.

Ao contrário das ferramentas de scaffolding, os kits de inicialização são relevantes apenas para o projeto inicial. Após a instalação, você provavelmente não usará esse kit novamente \(se for um bom kit de inicialização, talvez você volte a ler a documentação\).

Em relação ao Angular, a maneira mais fácil de começar é o Angular-CLI, que é uma ferramenta de scaffolding. Vamos abordar o seu uso neste tutorial.

Neste capítulo, mostramos todos os arquivos e pastas criados pelo Angular-CLI quando você cria um novo projeto. Começaremos com uma ação importante: alterando o prefixo do aplicativo.

### Prefixo de aplicação

O prefixo é usado para diferenciar os componentes que você cria em sua aplicação dos componentes de outras fontes e de componentes HTML. Você pode dar suas iniciais como o prefixo se for um projeto pessoal. Se você está colaborando ou trabalhando para um cliente, você pode ter as iniciais do nome do projeto como o prefixo. Neste tutorial, o prefixo simplesmente será `todo`.

O Angular-CLI gera um arquivo de configuração para uso próprio: `angular.json`. Abra este arquivo, encontre a propriedade `prefix` e altere seu valor de` app` para `todo`. De agora em diante, cada componente e diretiva que você criará usando Angular-CLI terá esse prefixo em seu seletor.

{% hint style="info" %}
Quando você alterar seu prefixo, você tem que mantê-lo em mente pelo restante do tutorial!
{% endhint %}

Poderíamos ter definido o prefixo quando criamos o projeto, adicionando `--prefix <prefixo>`. Então, mesmo o componente raiz que é gerado teria esse prefixo. Mas estamos bem com seu seletor atual, `app-root`, e não o mudaremos neste momento. 

### Estrutura da Aplicação

A primeira coisa a fazer quando você trabalha com o CLI é o projeto inicial do scaffold. Para fazê-lo, você pode usar o comando (no terminal) `ng new <nome-do-projeto>` e o Angular-CLI criará a pasta para você e irá inicializar o projeto e irá fazer o download de todas as dependências necessárias.

Depois de criarmos o projeto, teremos um projeto nesse formato


```text
├── angular.json // configuração Angular CLI
├── e2e // teste end-to-end
├── karma.conf.js // arquivo de configuração de teste
├── package.json // arquivo de configuração de pacotes
├── protractor.conf.js // arquivo de configuração de teste
├── README.md // seu readme
├── src // seu código vem aqui
│   ├── app
│   │   ├── app.component.css
│   │   ├── app.component.html
│   │   ├── app.component.spec.ts
│   │   ├── app.component.ts
│   │   ├── app.module.ts
│   │   └── index.ts
│   ├── assets // imagens etc
│   ├── environments // variáveis de ambiente
│   │   ├── environment.prod.ts
│   │   └── environment.ts
│   ├── favicon.ico // ícone para o navegador
│   ├── index.html
│   ├── main.ts
│   ├── polyfills.ts
│   ├── styles.css
│   ├── test.ts
│   ├── tsconfig.json // configuração typescript
│   └── typings.d.ts
└── tslint.json // configuração linting
```

Vamos ignorar todos os arquivos de configurações por agora e pular diretamente para a estrutura da pasta. O aplicativo (app) é o principal componente da aplicação e é a partir desse ponto em que iniciamos o nossa aplicação.
Vamos abordar os componentes mais detalhadamente no próximo tutorial, mas a principal idéia do projeto é que criamos componentes e os conectarmos até ter uma aplicação.

Com o Angular-CLI podemos gerar componentes e alguns outros arquivos que podem nos ajudar no futuro. Para fazê-los, devemos escrever `ng generate component <nome-do-componente>` para componentes e `ng generate route <caminho da rota>` para rotas e muitos mais que podem ser revisados ​​em [documentação do angular cli](https://angular.io/cli/generate).

Agora, você provavelmente pergunta como você pode acessar e testar sua aplicação?
Para isso, você deverá rodar o comando `ng serve` e acessar sua aplicação em `http://localhost:4200` e por último, mas não menos importante, se você quer enviar seu projeto para produção, você deve usar o comando `ng build`.
