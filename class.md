# Class


##class definition 
class is a special function that can be instantiated (create multiple copies from definition)
there are three parts in class 

1.properties (define variables of the class)
2.methods (functions for the class)
3.constructor (function that initializes the class)

#in Angular...

```ts
import { TodoListService } from '../todo-list.service';
```

we use the **import** statment to bring dependencies such as  TodoListService
which we will use in the constructor...
angular automatically makes an instance of the service for us.
This happened in the constructor where we define 
```private todoListService:TodoListService ```



in order to use ngOnint (part of the component life cycle) we need to implements the OnInit interface 

.
.
.
```export class ListManagerComponent implements OnInit {
  private title:string = 'My Todos';
  private todoList;
  constructor(private todoListService:TodoListService) {
  }
  ngOnInit() {
    this.todoList = this.todoListService.getTodoList();
  }
```




