# Installation

Every developer needs a set of tools and libraries before start working. In our case, we'll install all necessary tools together and once we have our Angular-CLI installed, it will take care of additional libraries we'll need for current and future projects.

## Tools

### Browser

Our first tool is the **browser**. We'll use it to see the result of our work and debug it. We recommend [Google Chrome](https://www.google.com/chrome/browser/desktop/) - it has great developer tools. [Firefox](https://www.mozilla.org/en-US/firefox/new/) is also awesome. If you don't already have one of those, just click the relevant link and follow the instructions to download and install the browser you choose.

### IDE

Our next tool is the **IDE** -  integrated development environment. It's a software that helps you write the code. IDEs can do a lot of amazing things such as:

* paint the code so it's easier to identify expressions
* suggest completions to what you type
* helps navigate easily through the files in your project
* and a lot more...

JetBrains [Webstorm](https://www.jetbrains.com/webstorm/download/) is one of the strongest IDE's in the market. You get the first month for free, and a totally free license if you're a student.

Microsoft [Visual Studio Code](https://www.visualstudio.com/vs/) is also a great choice that gains a lot of popularity lately. It is completely free for individuals.

Choose the IDE you'd like to work with and follow the installation instructions in its website.

### Git

Git is a tool that helps you manage versions of your code and work in collaboration with team members. There is a lot to know about it, but in this tutorial we will cover only basic usage.

You can download it and follow the installation instructions [here](https://git-scm.com/) .

### Github

[Github](https://github.com/) is a code repository website, which integrates with Git. It allows you to publish your project on the Web, copy other open source projects and collaborate. To be able to publish your project, make sure you create a user in Github's website (for free of course).

### NodeJS and NPM

Another tool which most web developers are using is **NodeJS**. Once installed, it comes with another tool called **NPM** (Node Package Manager).

NodeJS lets you run JavaScript code on your computer. It's used to run a local server which serves the project files to the browser and then simulates a real running website.

NPM allows you to easily download and install different libraries from the internet and also manage their versions.

Download NodeJS [here](https://nodejs.org/en/).

If you already have NodeJS installed, make sure you check that the version is greater than 4.0 by running this in your command line / terminal:   
```
node -v
```
\('-v' stands for 'version'.\)  

If it's lower than 4.0, download the new version from the website and install it.

Once installed, you should also have NPM installed. Check its version by running:  
```
npm -v
```


### Angular-CLI

[Angular-CLI](https://github.com/angular/angular-cli) is a powerful tool that simplify a lot the development process. It also installs libraries you'll use in your current and future projects. Install it by running:
```
npm i -g angular-cli
```

This command runs the NPM we recently installed here - it knows where to find the package (angular-cli) you're looking for by the name of the package you provide.
the 'i' parameter, is a short form of 'install'.
the '-g' parameter, stands for the word 'global' - we'd like to have this tool globaly installed on the computer, so that we could use it from any folder to any future projects.

Read more about Angular-CLI in the following section.

### Creating a Project

First, create a folder to store all your projects, for example _myProjects_, and then go into the folder, using a terminal (command line window):
```
cd the-path-to-your-folder/myProjects
```

Now, create a new project, called _todo-list_ inside the projects folder, using Angular-CLI, by running the following command:
```
ng new todo-list
```
This can take a while, since many packages are being downloaded and installed.


Now enter the new folder that Angular-CLI created for this project
```
cd todo-list
```
Once inside the folder of the application, run the application by using the following command:
```
ng serve
```
Now open your web browser and enter the URL - `localhost:4200`

You should see the title **App works!**



### Congratulations!

You have a running Angular application!  
To stop it from running, press `Ctrl+C` in the terminal.
As long as it's running, any change you make in the project code, it will be reflected immediately in the web browser.

Now we're ready to start with our project!

