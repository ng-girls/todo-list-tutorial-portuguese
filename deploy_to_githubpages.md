# \#20: 🛰 Deploy para o GitHub Pages

{% hint style="info" %}
**Instruções para o StackBlitz** ![](assets/stackblitz-hint.svg)

Siga as instruções da página referente ao [StackBlitz](stackblitz.md) para renomear o seu projeto e compartilhar o link da sua aplicação.
{% endhint %}

Para fazer o deploy das suas alterações para o GitHub Pages, nós usaremos o pacote angular-cli-ghpages:
[https://github.com/angular-schule/angular-cli-ghpages](https://github.com/angular-schule/angular-cli-ghpages).

Para realizamos esse processo, temos alguns requisitos:

* Você precisa ter um usuário no GitHub;
* Você precisa criar um repositório para o seu projeto;
* Você precisa fazer um commit de todas as alterações do projeto;
* Você precisa instalar o angular-cli-ghpages.

## Criando um usuário no GitHub

Se você já possui um usuário no GitHub, pode pular esse passo. Para criar um usuário, acesse  [https://github.com/](https://github.com/). Preencha o formulário de cadastro e certifique-se de validar seu endereço de e-mail.

## Criar um repositório de seu APP

Depois de fazer o login no GitHub, clique no botão `Start a project`, e dê o nome do repositório de `ng-girls-todo` ou qualquer outro que desejar.

_**Dica**_ O GitHub Pages é case sensitive. Nesse caso, é melhor utilizar letras minúsculas para nomear o repositório.

## Conectando seu repositório

Faça um commit de todas as suas alterações executando o seguinte comando na pasta do seu projeto:

```text
git add -A && git commit -m "Your Message"
```

Execute este comando para conectar seu código ao repositório, certificando-se de substituir o {YOUR\_USERNAME} e o {YOUR\_REPO} com o seu usuário do GitHub e o nome do repositório:

```text
git remote add origin https://github.com/{YOUR_USERNAME}/{YOUR_REPO}.git
git push -u origin master
```

## Fazendo deploy para o GitHub Pages

Primeiro, instale o angular-cli-ghpages:

```text
npm i -g angular-cli-ghpages
```

Então execute o comando:

```text
ng build --prod --base-href="/[your-repo-name]/"
angular-cli-ghpages --dir=dist/todo-list
```
💡 `./[your-repo-name]` é um placeholder para o nome do seu repositório no GitHub. Sendo assim, caso o seu projeto esteja em  `https://github.com/myname/ng-girls`, o valor será `--base-href="./ng-girls"` . Em outros sistemas operacionais, também pode ser "/ng-girls/".

Seu app estará disponível em [https://\[your-GH-username\].github.io/\[repo-name\]/](https://[your-GH-username].github.io/[repo-name])

Para mais informações, veja [https://github.com/angular-schule/angular-cli-ghpages](https://github.com/angular-schule/angular-cli-ghpages).

## Problemas conhecidos

### Tela branca \(e erro 404 no DevTools do Browser\)

Se o deploy ocorreu com sucesso, mas apareceu uma tela branca no browser, provavelmente foram utilizadas letras maiúsculas no nome do seu repositório. Tente criar um novo, contendo apenas letras minúsculas. Depois, remova a conexão antiga no seu ambiente local:

```text
git remote rm
```

Crie a conexão com o novo repositório:

```text
git remote add origin https://github.com/{YOUR_USERNAME}/{YOUR_REPO}.git
git push -u origin master
```

Faça um novo build:

```text
ng build --prod --base-href="/[your-repo-name]/"
angular-cli-ghpages --dir=dist/todo-list
```


### Problemas no Windows

Em algumas máquinas \(windows\) você pode se deparar com um erro como esse:

```text
An error occurred!
 Error: Unspecified error (run without silent option for detail)
    at C:\Users\<myuser>\AppData\Roaming\nvm\v8.9.1\node_modules\angular-cli-ghpages\node_modules\gh-pages\lib\index.js:232:19
    at _rejected (C:\Users\<myuser>\AppData\Roaming\nvm\v8.9.1\node_modules\angular-cli-ghpages\node_modules\q\q.js:844:24)
    ...
```

Tente debugá-lo com `angular-cli-ghpages -S` . Você pode obter o seguinte problema:

```text
fatal: could not read Username for \'https://github.com\': No error\n',
```

Nesse caso, execute estes passos:

1. Crie um Personal Access Token através deste link: [https://github.com/settings/tokens](https://github.com/settings/tokens)
2. Execute o comando a seguir, informando o token, repositório, username e e-mail:

   ```text
   angular-cli-ghpages --repo=https://<personal-access-token>@github.com/organisation/your-repo.git --name="Displayed Username" --email=mail@example.org
   ```
