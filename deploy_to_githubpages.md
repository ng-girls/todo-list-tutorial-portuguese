# Deploy to GithubPages

By deploying to Github pages your app will have a host and will live and run on the Web. Everyone will be able to see and use it. 

Angular-CLI makes it really easy for us to deploy to Github Pages - you can do so with a single command. But you have to prepare a few things first:

* You need to have a Github user
* You need to connect your Github user to your computer using a key
* You need to commit all the changes you made in the project

After completing these steps, run this command: 

```
ng github-pages:deploy --message "Deploying first version to Github Pages"
```

You will be asked to create and connect a Github repository for your project. This will happen only in the first time you deploy. 
