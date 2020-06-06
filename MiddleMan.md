# Middle Man
## Reasons
If a class performs only one action, delegating work to another class, why does it exist at all?

## Solutions
### Remove Middle Man
```js
// Bad
class Client {
  //...
  makeOrder() {
    this.manager.performWork();
  }
}

class Manager {
  //...
  performWork() {
    this.worker.performWork();
  }
}

class Worker {
  //...
  performWork() {
    //...
  }
}

// Better
class Client {
  //...
  makeOrder() {
    this.worker.performWork();
  }
}

class Worker {
  //...
  performWork() {
    //...
  }
}
```
