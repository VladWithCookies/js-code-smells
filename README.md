# JS code smells

## Too Many Parameters
Functions can have too many parameters. If they have too many, it makes the function more complicated when reading it and calling it. It probably means that we can clean up the code in some way to make this easier to read and use.

```js
// Bad
const describeFruit = (color, name, size, price, numSeeds, type) => {
  return `${fruitName} is ${fruitColor}. It's ${fruitSize}. It costs ${price}. It has ${numSeeds}. The type if ${type}`;
}

// Better
const describeFruit = ({ name, color, size, price, seedsCount, type }) => {
  return `${name} is ${color}. It's ${size}. It costs ${price}. It has ${seedsCount}. The type is ${type}`;
}
```

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

## Duplicate code
This is a problem because we have to change multiple pieces of code when we have to change duplicate code. Also, it’s easy to forget that they’re there by other developers.

This is why the don’t repeat yourself (DRY) principle is emphasized a lot. It saves developers time.

## Complexity
If there’s a simpler solution, we should go for that instead of writing something more complex.

## Shotgun Surgery
Shotgun surgery is a change that requires code to be multiple pieces of code to be changed.

```js
// Bad
const express = require('express');
const bodyParser = require('body-parser');
const app = express();

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.get('/foo', (req, res) => {
  console.log('foo called');
  res.json({ message: 'foo' });
});

app.get('/bar', (req, res) => {
  console.log('bar called');
  res.json({ message: 'bar' });
});

app.get('/baz', (req, res) => {
  console.log('baz called');
  res.json({ message: 'baz' });
});

app.listen(3000, () => console.log('server started'));

// Better
const express = require('express');
const bodyParser = require('body-parser');
const app = express();

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.use((req, res, next) => {
  if (req.path.substring(1)) {
    console.log(`${req.path.substring(1)} called`);
  }
  
  next();
});

app.get('/foo', (req, res) => res.json({ message: 'foo' }));
app.get('/bar', (req, res) => res.json({ message: 'bar' }));
app.get('/baz', (req, res) => res.json({ message: 'baz' }));
app.listen(3000, () => console.log('server started'));
```

## Large Classes
Any class that’s large is going to be hard to maintain. Classes are supposed to create objects that only do one thing. We don’t want classes that are so big that they’re doing many things.

```js
// Bad
class Employee {
  eat() {
    console.log('eating');
  }
  
  drink() {
    console.log('drinking');
  }
  
  work() {
    console.log('working');
  }
  
  sleep() {
    console.log('sleeping');
  }
  
  walk() {
    console.log('walking');
  }
}

// Better
class Person {
  eat() {
    console.log('eating');
  }
  
  drink() {
    console.log('drinking');
  }
  
  sleep() {
    console.log('sleeping');
  }
  
  walk() {
    console.log('walking');
  }
}

class Employee extends Person {
  work() {
    console.log('working');
  }
}
```

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

## Lazy or Freeloader Class
A lazy or freeloader class is a class that does too little. If it doesn’t do much, it probably shouldn’t be added since it’s mostly useless.

We should find a way to put whatever is in the lazy class into a place that has more stuff. A class that has only one or two methods probably isn’t too useful.

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

## Data Clump
A data clump is a situation where we have too many variables passed around together in various parts of a program. This means that we should group these together into their own objects and pass them together.

```js
// Bad
let fruitColor = 'red';
let fruitName = 'apple';
let fruitSize = 'small';
let fruitPrice = 1;
let fruitNumSeeds = 2;
let fruitType = 'Granny Smith';

const describeFruit = (color, name, size, price, seedsCount, type) => {
  return `${fruitName} is ${fruitColor}. It's ${fruitSize}. It costs ${price}. It has ${seedsCount}. The type is ${type}`;
}

describeFruit(fruitColor, fruitName, fruitSize, fruitPrice, fruitNumSeeds, fruitType);

// Better
let fruit = {
  color: 'red',
  name: 'apple',
  size: 'small',
  price: 1,
  numSeeds: 2,
  type: 'Granny Smith'
};

const describeFruit = ({ name, color, size, price, seedsCount, type }) => {
  return `${name} is ${color}. It's ${size}. It costs ${price}. It has ${seedsCount}. The type is ${type}`;
}

describeFruit(fruit);
```

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
}```
