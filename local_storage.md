# Local storage

## What is local storage?

Local storage, as it's name implies, is a tool for storing data locally.  
As similar to cookies, local storage stores the data on the user's computer, and by that it lets us, as developers, a quick way to access this data for both reading and writing.

## Browser support

As local storage was first introduced to us along with HTML5, all browsers that support HTML5 standard will also support local storage.  
Basically it is supported by most modern web browsers, including IE 8.

## We want to see some code!

First, in order to use local storage, we can simply access a localStorage instance which is exposed to us globally.  
That means that we can call all available methods in this interface by simply using this instance.

Local storage stores the data in a form of key-value, so the interface is quite-simple and has two main methods: `getItem` and `setItem`.

An example usage:

```
localStorage.setItem('name','Mor');

let name = localStorage.getItem('name'); 
alert('Hello '+name+'!');
```

Another useful method is `clear` and it is used to clear the local storage from data:

`localStorage.clear();`

There are a few more wonderful methods you can use, as described [here](https://developer.mozilla.org/en-US/docs/Web/API/Storage).

## Angular time \(back to our app\)

In the following section we will build a local storage service that later on will be used to store our todo list items.  
As described in earlier tutorials, we will generate the service using `angular-cli`:

```
$ ng g s todo-list-storage
```

The new file `todo-list-storage.service.ts`, should be created with the following code:

```
import { Injectable } from '@angular/core';

@Injectable()
export class TodoListStorageService {

  constructor() { }

}
```

**If something looks unfamiliar/odd to you, please refer to the [Service tutorial](https://shmool.gitbooks.io/todo-list-tutorial/content/service.html) for more detailed information about services.**

We need to provide the service in our ngModule. Open `app.module.ts` and in the `providers` list add the new class:
```ts
providers: [TodoListService, TodoListStorageService],
```
Make sure the class is also imported into the file:
```ts

import { TodoListStorageService } from './todo-list-storage.service';
```

Lets start by adding a private property to our service `todoList` which will hold the list items.

`private todoList;`

In addition, let's add a constant that will store the name of the key we want to use for our local storage, add it right after the imports:

`const storageName = 'aah_todo_list';`

Now we want to initiliaze this property with data, by retriving it from localStorage, so within the constructor, add:
```ts
constructor() {  
    this.todoList = JSON.parse(localStorage.getItem(storageName));  
}
```

Wait! Wait! why `JSON.parse`? The answer is simple:
As described earlier in this tutorial, local storage stores data in a form of key-value, that means that the values are stored as **strings**.  
So, if we want to have a real object to deal with, we must parse the strign into a valid object.

Now lets start doing some real stuff, but first we will declare all the public methods we want to expose in this service, which are **get, post, put**, and **destroy**.  
Our service should now look similiar to:

```
import { Injectable } from '@angular/core';

const storageName = 'aah_todo_list';

@Injectable()
export class TodoListStorageService {

  private todoList;

  constructor() {
    this.todoList = JSON.parse(localStorage.getItem(storageName));
  }

  // get items
  get() {}

  // add a new item
  post(item) {}

  // update an item
  put(item, changes) {}

  // remove an item
  destroy(item) {}

}
```

We will now implement them one by one.

### get

This method will simply return the current state of items stored in the service:

```
/**
   * get items
   * @returns {any[]}
   */
  get() {
    return [...this.todoList];
  }
```

If you are not familiar with the `...` operator, please refer to [this documentaion](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Spread_operator) for more information.

### post

This method will be responsible for adding a new item, and returning the new list.  
It accepts one parameter, `item` which will be the item to add:

```
/**
   * Add a new todo item
   * @param item
   * @returns {any[]}
   */
  post(item) {
    this.todoList.push(item);
    return this.get();
  }
```

Some of you might notice that we just pushed a new item to the array.  
But what about the local storage? we must also syncornize it with the new array!

Lets add a new **private** method in our service, which will be used internaly to update the stored list:

```
/**
   * Syncronize the local storage with the current list
   * @returns {any[]}
   */
  private update() {
    localStorage.setItem(storageName, JSON.stringify(this.todoList));

    return this.get();
  }
```

Lets explain.  
Here we use the simple method of `setItem`, which takes a key \(first argument\) and a string value \(second argument\) and stores it in the local storage.  
After we updated the value, we simply return the new list using the `get` method we implemented earlier.

Now we need to modify our `post` function to use `update` so everyhing is syncronized in harmony:

```
/**
   * Add a new todo item
   * @param item
   * @returns {any[]}
   */
  post(item) {
    this.todoList.push(item);
    return this.update();
  }
```

### put

Here we want to update an existing item.  
Before that, let's add another helper private method `findItemIndex`, which will simply return the index of an item with the list array:

```
/**
   * find the index of an item in the aray
   * @param item
   * @returns {number}
   */
  private findItemIndex(item) {
    return this.todoList.indexOf(item);
  }
```

Now, we can use `Object.assign` to update an existing item:

```
/**
   * Update an existing item
   * @param item
   * @param changes
   * @returns {any[]}
   */
  put(item, changes) {
    Object.assign(this.todoList[this.findItemIndex(item)], changes);
    return this.update();
  }
```

So what is going on here?   
`Object.assign` takes a target object \(first argument\) and source objects \(all the rest of the argument\), and copies to the target object.  
If a property existing on both target and source, this method will replace the old value with the new one.  
Here we want to update an item in the list, so first we find it's index in the array, and then apply the changes on it.  
At the end, we want to syncronize the local storage \(`this.update`\) and return the new list.

### destroy

This method will remove an item from the list and then syncronize with local storage:

```
/**
   * Remove an item from the list
   * @param item
   * @returns {any[]}
   */
  destroy(item) {
    this.todoList.splice(this.findItemIndex(item), 1);
    return this.update();
  }
```

The above code is quite simple.  
`splice(i, n)` removes `n` items starting from index `i`.  
In our code, we first find the index of the item to remove, and remove only it \(that's why we use 1 as the second parameter\).

## Add some default data

Lets assume we want our todo list always have some default data to start with.   
Then we can add it by modifying our service, by adding in the constants section \(after the imports\):

```
const defaultList = [
  { title: 'install NodeJS' },
  { title: 'install Angular CLI' },
  { title: 'create new app' },
  { title: 'serve app' },
  { title: 'develop app' },
  { title: 'deploy app' },
];
```

And then modify our constructor:

```
constructor() {
    this.todoList = JSON.parse(localStorage.getItem(storageName)) || defaultList;
  }
```

The above will make sure that if data was not yet set to localStorage, our service will still have some default data to return.

## Almost done!

Our service is now ready for work!   
But wait, we need to provide it, in order to use it.

Open `app.module.ts` and add `TodoListStorageService` to the `providers` array.  
Now we are trully ready to use the service!

Now for our app to use the new local storage service, let's open up `todo-list.service.ts` and modify it.

First we need to import the new service:

`import { TodoListStorageService } from './todo-list-storage.service';`

Then, we need to inject it in the constructor so we will have an instance to work with:

```
constructor(private storage:TodoListStorageService) {
}
```

This will let us use `this.storage` across the todo-list service.

Let's also modify the current methods:

**Before**

```
getTodoList() {
    return this.todoList;
}

addItem(item) {
    this.todoList.push(item);
}
```

**After**

```
getTodoList() {
    return this.storage.get();
}

addItem(item) {
    return this.storage.post(item);
}
```

Now we have one last modification to make. Open up `list-manager.component.ts`, and let's modify `addItem` method this way:

```
addItem(title:string) {
    this.todoList = this.todoListService.addItem({ title });
}
```

The above change will make sure that when we add a new item, our list will also be updated visually.

## Summary

In this tutorial we learned what is localStorage and how to use it.  
We saw that localStorage is a great and a pretty straight-forward tool for developers to store data locally on the users' computers/devices.  
We then implemented a new service that uses localStorage to store the todo-list items, and updated the rest of the components to support this new service.

Enjoy the rest of the tutorial!

