# \#20: 🛰 Deploy para o GitHub Pages

Esta é uma versão antiga - precisamos verificar isso :\) 

Para fazer o deploy das suas alterações para o GitHub Pages nós usaremos o pacote do angular-cli-ghpages
[https://github.com/angular-buch/angular-cli-ghpages](https://github.com/angular-buch/angular-cli-ghpages)

* Você precisa ter um usuário no GitHub
* Você precisa criar um repositório para o seu projeto.
* Você precisa fazer um commit de todas as alterações que você fez no projeto
* Você precisa instalar o angular-cli-ghpages

## Criando um usuário no GitHub

Se você já possui um usuário no GitHub pode pular esse passo. Para criar um usuário no Github, vá para o GitHub: [https://github.com/](https://github.com/). Preencha o formulário de cadastro e certifique-se de validar seu endereço de e-mail.

## Criar um repositório de seu APP

Depois de fazer o login no GitHub, clique no botão `Start a project`, e dê o nome do repositório de `ng-girls-todo` ou qualquer outro nome que desejar.

## Conectando seu repositório

Faça um commit de todas as suas alterações executando o seguinte comando na pasta do seu projeto.

```text
git add -A && git commit -m "Your Message"
```

Execute o seguinte comando para conectar seu código ao repositório. Certifique-se de substituir o {YOUR\_USERNAME} e o {YOUR\_REPO} com o seu usuário do GitHub e o nome do repositório.

```text
git remote add origin https://github.com/{YOUR_USERNAME}/{YOUR_REPO}.git
git push -u origin master
```

## Fazendo deploy para o GitHub Pages

Primeiro, instale angular-cli-ghpages.

```text
npm i -g angular-cli-ghpages
```

Então execute o comando:

```text
ng build --prod --base-href="/[your-repo-name]/"
angular-cli-ghpages
```

Seu app estará disponível em \[[https://\[your-GH-username\].github.io/\[repo-name\]\(https://\[your-GH-username\].github.io/\[repo-name\)\](https://[your-GH-username].github.io/[repo-name]%28https://[your-GH-username].github.io/[repo-name%29\)\]

Para mais informações veja [https://github.com/angular-buch/angular-cli-ghpages](https://github.com/angular-buch/angular-cli-ghpages).

## Problemas conhecidos

Em máquinas \(windows\) você provavelmente vai se deparar com um erro como esse:

```text
An error occurred!
 Error: Unspecified error (run without silent option for detail)
    at C:\Users\<myuser>\AppData\Roaming\nvm\v8.9.1\node_modules\angular-cli-ghpages\node_modules\gh-pages\lib\index.js:232:19
    at _rejected (C:\Users\<myuser>\AppData\Roaming\nvm\v8.9.1\node_modules\angular-cli-ghpages\node_modules\q\q.js:844:24)
    ...
```

Tente debugá-lo com `angular-cli-ghpages -S` . Se você obter o seguinte erro:

```text
fatal: could not read Username for \'https://github.com\': No error\n',
```

você pode fazer o seguinte

1. Criar um Personal Access Token aqui: [https://github.com/settings/tokens](https://github.com/settings/tokens) e insira este token de acesso ao seu repositório!
2. Execute o seguinte comando e substitua seu token, organisation \(your user\), repositório, username e email:

   ```text
   angular-cli-ghpages --repo=https://<personal-access-token>@github.com/organisation/your-repo.git --name="Displayed Username" --email=mail@example.org
   ```
