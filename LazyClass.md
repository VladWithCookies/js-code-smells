# Lazy Class
## Reason
Understanding and maintaining classes always costs time and money. So if a class doesn’t do enough to earn your attention, it should be deleted.

## Solutions
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
