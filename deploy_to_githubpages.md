 # Deploy your App to Github Pages
To deploy our changes to Github pages we will use the angular-cli-ghpages package
https://github.com/angular-buch/angular-cli-ghpages 

* You need to have a Github user
* You need to create a repostiroy for your project.
* You need to commit all the changes you made in the project
* You need to install angular-cli-ghpages

## Creating a Github user
If you already have a Github user you can skip this step.
To Create a Github user go to Github: https://github.com/
Fill the regetration form and make sure to validate your email address.

## Create your App repository
After logging in to Github.
Click on the `Start a project` button, and name the repository `ng-girls-todo` or any other name you like.

## Connecting your repository

Commit all your changes by runing this command in your project directory.
```
git add -A && git commit -m "Your Message"
```

Run the following command to connect your code to your repository.
make sure to replace the {YOUR_USERNAME} and {YOUR_REPO} with your github username and repository name.
```
git remote add origin https://github.com/{YOUR_USERNAME}/{YOUR_REPO}.git
git push -u origin master
```

## Deploying to Github Pages
First install angular-cli-ghpages.
```
npm i -g angular-cli-ghpages
```
Then Simply Run:
```
ng build --prod
angular-cli-ghpages
```
For more information see https://github.com/angular-buch/angular-cli-ghpages.
