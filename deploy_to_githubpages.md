 # Fazer o deploy do seu App para o Github Pages
Para fazer o deploy das suas alterações para o Github pages nós usaremos o pacote do angular-cli-ghpages
https://github.com/angular-buch/angular-cli-ghpages 

* Você precisa ter um usuário no Github
* Você precisa criar um repositório para o seu projeto.
* Você precisa fazer um commit de todas as suas alterações que você fez no projeto
* Você precisa instalar o angular-cli-ghpages

## Criando um usuário no Github
Se você já possui um usuário no Github você pode pular esse passo.
Criar um usuário no Github: https://github.com/
Preencha o formulário de registro e faça a validação de seu e-mail

## Criar um repositório de seu APP
Depois de fazer o login no Github.
Click no botão `Start a project`, e dê o nome do repositório de `ng-girls-todo` ou qualquer outro nome que você desejar.

## Conectando seu repositório

Faça um commit de todas as suas alterações rodando o seguinte comando na pasta do seu projeto.
```
git add -A && git commit -m "Your Message"
```

Rode o seguinte comando para conectar seu código ao seu repositório.
Não esqueça de trocar o {YOUR_USERNAME} e {YOUR_REPO} com o seu usuário do github e o nome do repositório.
```
git remote add origin https://github.com/{YOUR_USERNAME}/{YOUR_REPO}.git
git push -u origin master
```

## Fazendo o deploy para o Github pages 
Primeiro, faça a instalação do angular-cli-ghpages.

```
npm i -g angular-cli-ghpages
```

Então rode:

```
ng build --prod --base-href="/[your-repo-name]/"
angular-cli-ghpages
```

Seu app estará disponível em: https://[your-GH-username].github.io/[repo-name]

Para mais informações veja: https://github.com/angular-buch/angular-cli-ghpages.
