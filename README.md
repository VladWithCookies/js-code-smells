# JS code smells
## Duplicate code
TODO

## Complexity
TODO

## Shotgun Surgery
TODO

## Large Classes
TODO

## Feature Envy
Feature envy means that one class uses too many features of another class. This means that most of one class reference something in another class.

Example: 
```
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

## Inappropriate Intimacy
A class that has dependencies on the implementation details of another class is considered to be too intimate.

We don’t want classes that depend on the implementation of the other classes because this means that we have to change both classes when the first class change.

There isn’t enough encapsulation of the fields or implementation of the methods.

The lack of encapsulation may arise from exposing the fields of the class. Letting us set field values directly is probably not good in most cases.

Example:
```
// Bad
class Box {
  constructor() {
    this.length = 1;
    this.width = 1;
    this.height = 1;
  }
  
  getSurfaceArea() {
    return 2 * (this.height * this.width) + 2 * (this.height * this.length) + 2 * (this.length * this.width)
  }
}

class ShapeCalculator {
  constructor() {
    this.box = new Box();
  }
  
  getBoxSurfaceArea() {
    return this.box.getArea();
  }
  
  getBoxVolume() {
    return this.box.length * this.box.width * this.box.height;
  }
}

//Better 
TODO
```
