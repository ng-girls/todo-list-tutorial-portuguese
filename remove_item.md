# Remove item

The user should be able to remove any item, whether it's still active or completed. Revoving an item will be done by clicking a button, aptly named "remove". In this tutorial, we'll learn how to add this functionality to our project.

(1) First, we need to add the button to the item, so we'll work on the file *item.component.ts*.

(a) Add the **remove** button to template, right next to the end of the main *<div>* element:
```
<button class="btn btnRed" (click)="removeItem()">
  remove
</button>
```

(b) Add a new output to the ItemComponent class, which will be emitted to the list manager when a user pressed the remove button for a specific item:
```
@Output() remove:EventEmitter<any> = new EventEmitter();
```

(c) Add a function to the ItemComponent class that will actually emit the event. This function will be called when the user clicks the **remove** button:
```
removeItem() {
  this.remove.emit(this.item);
}
```

(2) Now that each todo item can emit its own removal, let's make sure that the list manager actually removes that same item from the list. For that, we'll work on the file *list-manager.component.ts*.

(a) We need to respond to **remove** event - let's add it to the template, inside the *<todo-item>* tag:
```
(remove)="removeItem($event)"
```

(b) Now we just need to add the function *removeItem()* to the ListManagerComponent class:
```
removeItem(item) {
  this.todoList = this.todoListService.removeItem(item);
}
```
