# Divergent Change
## Reason
You find yourself having to change many unrelated methods when you make changes to a class. For example, when adding a new product type you have to change the methods for finding, displaying, and ordering products.

Often these divergent modifications are due to poor program structure or "copypasta programming”.

## Solutions
### Extract Class
```js
// Bad
class User {
  //...
  fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
  
  isAuthorized() {
    return this.isAdmin();
  }
}

// Better
class UserPresenter {
   //...
   fullName() {
    return `${this.firstName} ${this.lastName}`;
  }
}

class UserPolicy {
   //...
   isAuthorized(user) {
    return user.isAdmin();
  }
}
```
