# Data Clump
## Reason
A data clump is a situation where we have too many variables passed around together in various parts of a program. This means that we should group these together into their own objects and pass them together.

## Solutions
### Introduce Parameter Object
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

### Extract Class
```js
// Bad
class Person {
  name = 'Vlad';
  officeAreaCode = '+1';
  officeNumber = '2345678910';
  
  getTelephoneNumber() {
    return this.officeAreaCode.concat(this.officeNumber);
  }
}

// Better
class Person {
  name = 'Vlad';
  telephoneNumber = new TelephoneNumber();
  
  getTelephoneNumber() {
    return telephoneNumber.getTelephoneNumber();
  }
}

class TelephoneNumber {
  officeAreaCode = '+1';
  officeNumber = '2345678910';
  
  getTelephoneNumber() {
    return this.officeAreaCode.concat(this.officeNumber);
  }
}
```
