# Inappropriate Intimacy
## Reason
A class that has dependencies on the implementation details of another class is considered to be too intimate.

There isn’t enough encapsulation of the fields or implementation of the methods.

The lack of encapsulation may arise from exposing the fields of the class. Letting us set field values directly is probably not good in most cases.

## Solutions

```js
// Bad
class Box {
  constructor() {
    this.length = 1;
    this.width = 1;
    this.height = 1;
  }
  
  getArea() {
    return 2 * (this.height * this.width) + 2 * (this.height * this.length) + 2 * (this.length * this.width)
  }
}

class ShapeCalculator {
  constructor() {
    this.box = new Box();
  }
  
  getBoxArea() {
    return this.box.getArea();
  }
  
  getBoxVolume() {
    return this.box.length * this.box.width * this.box.height;
  }
}

// Better
class Box {
  constructor() {
    this.length = 1;
    this.width = 1;
    this.height = 1;
  }
  
  getArea() {
    return 2 * (this.height * this.width) + 2 * (this.height * this.length) + 2 * (this.length * this.width)
  }  
  
  getVolume() {
    return this.length * this.width * this.height;
  }
}

class ShapeCalculator {
  constructor() {
    this.box = new Box();
  }
  
  getBoxArea() {
    return this.box.getArea();
  }
  
  getBoxVolume() {
    return this.box.getVolume();
  }
}
```
