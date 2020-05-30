# Refused Bequest
## Reasons
Someone was motivated to create inheritance between classes only by the desire to reuse the code in a superclass. But the superclass and subclass are completely different.

## Solutions
### Replace Inheritance with Delegation
```js
// Bad
class Array {
  isEmpty() {
    //...
  }
}

class Stack extends Array {
  //...
}

// Better
class Array {
  isEmpty() {
    //...
  }
}

class Stack {
  array = new Array();
  
  isEmpty() {
    return this.array.isEmpty()
  }
}
```

### Extract Superclass
```js
// Bad
class Animal {
  legsCount = 4;
}

class Chair extends Animal {
  //...
}

// Better
class Legs {
  count = 4;
}

class Animal extends Legs {
  //...
}

class Chair extends Legs {
  //...
}
```
