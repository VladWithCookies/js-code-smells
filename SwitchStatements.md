# Switch Statements
## Reason
Relatively rare use of `switch` and case operators is one of the hallmarks of object-oriented code. Often code for a single `switch` can be scattered in different places in the program. When a new condition is added, you have to find all the `switch` code and modify it.

As a rule of thumb, when you see `switch` you should think of polymorphism.

## Solutions
### Replace Parameter with Explicit Methods
```js
// Bad
setValue(name, value) {
  swith name {
    case 'height':
      height = value;
      return;
    case 'width':
      width = value;
      return;
    case 'depth':
      depth = value;
      return;
    default:
      return;
  } 
}

// Better
setHeight(value) {
  height = value;
}

setWidth(value) {
  width = value;
}

setDepth(value) {
  depth = value;
}
```

### Replace Conditional with Polymorphism
```js
// Bad
class Bird {
  // ...
  getSpeed() {
    switch (type) {
      case EUROPEAN:
        return getBaseSpeed();
      case AFRICAN:
        return getBaseSpeed() - getLoadFactor() * numberOfCoconuts;
      case NORWEGIAN_BLUE:
        return (isNailed) ? 0 : getBaseSpeed(voltage);
    }
    
    throw new Error("Should be unreachable");
  }
}

// Better
class Bird {
  // ...
  getSpeed() {
    // ...
  };
}

class European extends Bird {
  getSpeed(): number {
    return getBaseSpeed();
  }
}

class African extends Bird {
  getSpeed(): number {
    return getBaseSpeed() - getLoadFactor() * numberOfCoconuts;
  }
}

class NorwegianBlue extends Bird {
  getSpeed(): number {
    return (isNailed) ? 0 : getBaseSpeed(voltage);
  }
}

// Somewhere in client code
let speed = bird.getSpeed();
```
