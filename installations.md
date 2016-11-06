# Installation

Every developer needs a set of tools and libraries to start working. In our case, we'll install all the tools, and Angular-CLI will take care of installing the libraries we'll need at this point.


## Tools


### Browser

Our first tool is the **browser**. We'll use it to see the result of our work and debug it. We recommend [Google Chrome](https://www.google.com/chrome/browser/desktop/) - it has great developer tools. [Firefox](https://www.mozilla.org/en-US/firefox/new/) is also awesome. If you don't already have one of those, just follow the link and the instructions to download the browser you choose.


### IDE

Our next tool is the **IDE** -  integrated development environment. It's a software that helps you write the code. IDEs can do a lot of amazing things: 
* show you all the files in the project, 
* paint the code so it's easier to identify each expression, 
* suggest completions to what you write, 
* and a lot more...

JetBrains [Webstorm](https://www.jetbrains.com/webstorm/download/) is a wonderful IDE. You get the first month for free, and a totally free license if you're a student.

Microsoft [Visual Studio](https://www.visualstudio.com/vs/) is also a great choice that gains a lot of popularity lately. It is free for individuals.

Choose the IDE you'd like to work with and follow the downloading instructions on its website. 


### Git
Git is a tool that helps you manage versions of your code, and work on a project with a team. There is a lot to know about it, but we will cover only minimal usage of Git in this tutorial.

Download it [here](https://git-scm.com/) and follow the installation instructions. 


### Github
[Github](https://github.com/) is a code repository which integrates with Git. It allows you to publish your project on the Web, use other open source projects, and collaborate. If you'd like to publish the project you're developing with this tutorial, and/or deploy it, make sure you have a Github user. 


### NodeJS and NPM

Another tool which most web developers use is **NodeJS**, which comes with **NPM** - Node Package Manager. 

NodeJS lets you run JavaScript code on your computer. It is used to run a local server which serves the project files to the browser.

NPM allows you to easily install libraries and manage their versions. 

Download NodeJS [here](https://nodejs.org/en/).

If you already have NodeJS installed, check if the version is greater than 4.0, by running this in your command line / terminal: 
```node -v```. ('-v' stands for 'version'.)
If it's lower than 4.0, download the new version from the website and install it.

Once installed, you should also have NPM. Check its version by running:
```npm -v```


### Angular-CLI

[Angular-CLI](https://github.com/angular/angular-cli) is a powerful tool that takes care of a lot of the development process, including installing libraries you'll use in your project. Install it by running: ```npm i -g angular-cli```. 

We're using the recently installed NPM here - it knows where to find the package you're looking for by the name of the package you provide. 'i' is a short form of 'install'. '-g' stands for 'global' - we'd like to have this tool globaly installed on the computer, so we can use it from any folder.

Read more about Angular-CLI in the following section. 
