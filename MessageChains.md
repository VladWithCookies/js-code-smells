# Message Chains
## Reasons
A message chain occurs when a client requests another object, that object requests yet another one, and so on. These chains mean that the client is dependent on navigation along the class structure. Any changes in these relationships require modifying the client.

## Solutions
### Hide Delegate
```js
// Bad
class Client {
  //...
  getManager() {
    const department = this.person.getDepartment();
    
    return department.getManager();
  }
}

class Department {
  //...
  getManager() {
    return this.manager;
  }
}

class Person {
  //...
  getDepartment() {
    return this.department;
  }
}

// Better
class Client {
  //...
  getManager() {
    return this.person.getManager();
  }
}

class Department {
  //...
  getManager() {
    return this.manager;
  }
}

class Person {
  //...
  getDepartment() {
    return this.department;
  }
  
  getManager() {
    return this.department.getManager();
  }
}
```
