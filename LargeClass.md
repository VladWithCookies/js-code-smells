# Large Class
## Reason
Any class that’s large is going to be hard to maintain. Classes are supposed to create objects that only do one thing. We don’t want classes that are so big that they’re doing many things.

## Solutions
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

### Extract Subclass
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
