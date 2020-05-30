# Alternative Classes with Different Interfaces
## Reason
Two classes perform identical functions but have different method names.
The programmer who created one of the classes probably didn’t know that a functionally equivalent class already existed.'

## Solutions
### Rename Methods
```js
// Bad
class Truck {
  drive() {
    //...
  }
}

class Car {
  takeARide() {
    //...
  }
}

// Better
class Truck {
  drive() {
    //...
  }
}

class Car {
  drive() {
    //...
  }
}
```

### Extract Superclass
```js
// Bad
class Truck {
  drive() {
    //...
  }
}

class Car {
  takeARide() {
    //...
  }
}

// Better
class Vehicle {
  drive() {
    //...
  }
}

class Truck extends Vehicle {
  //...
}

class Car extends Vehicle {
  //...
}
```
