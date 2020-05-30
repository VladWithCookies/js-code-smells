# LongMethod 
## Reason
Among all types of object-oriented code, classes with short methods live longest. The longer a method or function is, the harder it becomes to understand and maintain it.

In addition, long methods offer the perfect hiding place for unwanted duplicate code.

## Solutions
### Extract method
```js
// Bad
printOwing() {
  printBanner();

  console.log('name: ' + name);
  console.log('amount: ' + getOutstanding());
}

// Better
printOwing() {
  printBanner();
  printDetails(getOutstanding());
}

printDetails(outstanding) {
  console.log('name: ' + name);
  console.log('amount: ' + outstanding);
}
```

### Replace Temp with Query
```js
// Bad
calculateTotal() {
  const basePrice = quantity * itemPrice;
  
  if (basePrice > 1000) {
    return basePrice * 0.95;
  }
  
  return basePrice * 0.98;
}

// Better 
calculateTotal() {
  if (basePrice() > 1000) {
    return basePrice() * 0.95;
  }
  
  return basePrice() * 0.98;
}

basePrice() {
  return quantity * itemPrice;
}
```

### Replace Method with Method Object
```js
// Bad
class Order {
  // ...
  price() {
    let primaryBasePrice;
    let secondaryBasePrice;
    let tertiaryBasePrice;
    // Perform long computation.
  }
}

// Better 
class Order {
  // ...
  price(): number {
    return new PriceCalculator(this).compute();
  }
}

class PriceCalculator {
  _primaryBasePrice;
  _secondaryBasePrice;
  _tertiaryBasePrice;
  
  constructor(order) {
    // Copy relevant information from the
    // order object.
  }
  
  compute() {
    // Perform long computation.
  }
}
```

### Decompose Conditional
```js
// Bad
if (date.before(SUMMER_START) || date.after(SUMMER_END)) {
  charge = quantity * winterRate + winterServiceCharge;
} else {
  charge = quantity * summerRate;
}

// Better
const charge = isSummer(date) ? summerCharge(quantity) : winterCharge(quantity);
```
