# JS code smells
* Long method 
* Too Many Parameters

## Excessive Return of Data
Functions that return data we don’t need isn’t good. A function should only return what’s needed by outside code so that we don’t expose extra stuff that isn’t needed.

```js
// Bad
const getFruitColor = (fruit) => {
  return {
    ...fruit,
    size: 'big'
  };
}

// Better
const getFruitColor = (fruit) => fruit.color;
```

* Shotgun Surgery
* Large Classes
* Primitive Obsession

## Feature Envy
Feature envy means that one class uses too many features of another class. This means that most of one class reference something in another class.

Example: 
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

## Excessive Use of Literals
Using literals too much isn’t a good idea because repeating them will bring in more chances for errors. This is because we have to change each of them when we change code if there are too many of them.

```js
// Bad
const mediumRequest = fetch('http://medium.com');
const mediumJsUrl = 'https://medium.com/topic/javascript';

// Better
const MEDIUM_URL = 'http://medium.com';
const mediumRequest = fetch(MEDIUM_URL)
const mediumJsUrl = `${MEDIUM_URL}/topic/javascript`;
```

## Cyclomatic Complexity
Cyclomatic complexity means that there are too many conditional statements and loops in our code.

The complexity can arise in different ways. Loops and conditionals can be nested too deeply. More than two levels of nesting is probably too much and hard to read.

```js
// Bad
for (let f of foo) {
  if (Array.isArray(bar)) {
    for (let b of bar) {
      for (let z of baz) {
        //...
      }
    }
  }
}

// Better
const doSOmethignWithBaz = (baz) => {
  for (let z of baz) {
    //...
  }
}

for (let f of foo) {
  if (!Array.isArray(bar)) {
    continue;
  }
  
  for (let b of bar) {
    doSOmethignWithBaz(baz);
  }
}
```

## Orphaned Variable or Constant Class
These are classes that have a collection of constants that belong elsewhere rather than in their own class.

```js
// Bad
class Color {
  constructor() {
    this.apple = 'red';
  }
}

class Apple {
  constructor() {
    this.color = new Color().apple;
  }
}

// Better
class Apple {
  constructor() {
    this.color = 'red';
  }
}
```

* Data Clump

## Inappropriate Intimacy
A class that has dependencies on the implementation details of another class is considered to be too intimate.

There isn’t enough encapsulation of the fields or implementation of the methods.

The lack of encapsulation may arise from exposing the fields of the class. Letting us set field values directly is probably not good in most cases.

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
