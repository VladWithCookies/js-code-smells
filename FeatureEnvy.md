# FeatureEnvy
## Reason
Feature envy means that one class uses too many features of another class. This means that most of one class reference something in another class.

## Solutions
### Extract Method
```js
// Bad
class Rectangle {
  constructor() {
    this.height = 1;
    this.width = 1;
  }
}

class ShapeCalculator {
  constructor() {
    this.rectangle = new Rectangle();
  }
  
  getRectangleArea() {
    return this.rectangle.height * this.rectangle.width;
  }
}

// Better
class Rectangle {
  constructor() {
    this.height = 1;
    this.width = 1;
  }
  
  getArea() {
    return this.height * this.width;
  }
}

class ShapeCalculator {
  constructor() {
    this.rectangle = new Rectangle();
  }
  
  getRectangleArea() {
    return this.rectangle.getArea();
  }
}
```
