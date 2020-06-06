# Incomplete Library Class
## Reasons
The author of the library hasn’t provided the features you need or has refused to implement them.

## Solutions
### Introduce Foreign Method
```js
// Bad
class Report {
  // ...
  sendReport() {
    const nextDay = new Date(previousEnd.getYear(), previousEnd.getMonth(), previousEnd.getDate() + 1);
    // ...
  }
}

// Better
class Report {
  // ...
  sendReport() {
    const newStart = nextDay(previousEnd);
    // ...
  }
  
  static nextDay(arg) {
    return new Date(arg.getFullYear(), arg.getMonth(), arg.getDate() + 1);
  }
}
```

### Introduce Local Extension
```js
class NewClass extends LibraryClass {
  // ...
  usefullMethod() {
    // ...
  }
}
```
