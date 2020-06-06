# Speculative Generality
## Reasons
Sometimes code is created “just in case” to support anticipated future features that never get implemented. As a result, code becomes hard to understand and support.

## Solutions
### Collapse Hierarchy
```js
// Bad
class Employee {
  //...
  getSalary() {
    return this.salary
  }
}

class Salesman extends Employee {
  //...
  getSalary() {
    return this.salary
  }
}

// Better
class Employee {
  //...
  getSalary() {
    return this.salary
  }
}
```
### Inline Class
```js
// Bad
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

// Better
class Person {
  name = 'Vlad';
  officeAreaCode = '+1';
  officeNumber = '2345678910';
  
  getTelephoneNumber() {
    return this.officeAreaCode.concat(this.officeNumber);
  }
}
```
 
