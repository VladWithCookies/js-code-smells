# Data Class
## Reason
A data class refers to a class that contains only fields and crude methods for accessing them (getters and setters). These are simply containers for data used by other classes. These classes don’t contain any additional functionality and can’t independently operate on the data that they own.

## Solutions
### Move Method
```js
// Bad
class Name {
  //..
  getFirstName() {
    return this.firstName;
  }
  
  getLastName() {
    return this.lastName;
  }
}

class User {
  //...
}

// Better
class User {
  //..
  getFirstName() {
    return this.firstName;
  }
  
  getLastName() {
    return this.lastName;
  }
}
```
