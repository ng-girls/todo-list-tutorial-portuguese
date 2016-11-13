# Refactor App Component

We're going to perform a small refactoring. The app-root shouldn’t have such large template and all this logic. It should just call another component that will deal with that.

* Create a new component called list-manager: `ng g c list-manager -it`
* Move all the code from app-root to list-manager
* Call the new component from the app-root template: `<todo-list-manager></todo-list-manager>`

That's it! Now we can go on.

