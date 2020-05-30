# Temporary Field
## Reasons
Oftentimes, temporary fields are created for use in an algorithm that requires a large amount of inputs. So instead of creating a large number of parameters in the method, the programmer decides to create fields for this data in the class. These fields are used only in the algorithm and go unused the rest of the time.

This kind of code is tough to understand. You expect to see data in object fields but for some reason they’re almost always empty.

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
