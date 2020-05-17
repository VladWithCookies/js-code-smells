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

```js
// Bad
TODO

// Better
TODO
```

## Complexity
If there’s a simpler solution, we should go for that instead of writing something more complex.

```js
// Bad
TODO

//Better
TODO
```

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
