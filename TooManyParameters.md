# Too Many Parameters
## Reason
Functions can have too many parameters. If they have too many, it makes the function more complicated when reading it and calling it. It probably means that we can clean up the code in some way to make this easier to read and use.

## Solutions
### Introduce Parameter Object
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

### Replace Parameter with Method Call
```js
// Bad
class PriceCalculator() {
  getFees() {
    //...
  }
  
  getSeasonalDiscount() {
    //...
  }
  
  discountedPrice(basePrice, seasonDiscount, fees) {
    return basePrice - seasonDiscount + fees ;
  }
}

const priceCalculator = new PriceCalculator();
const basePrice = quantity * itemPrice;
const seasonDiscount = priceCalculator.getSeasonalDiscount();
const fees = priceCalculator.getFees();
const finalPrice = priceCalculator.discountedPrice(basePrice, seasonDiscount, fees);

// Better
class PriceCalculator() {
  getFees() {
    //...
  }
  
  getSeasonalDiscount() {
    //...
  }
  
  discountedPrice(basePrice) {
    const seasonDiscount = this.getSeasonalDiscount();
    const fees = this.getFees();
    
    return basePrice - seasonDiscount + fews;
  }
}

const priceCalculator = new PriceCalculator();
const basePrice = quantity * itemPrice;
const finalPrice = priceCalculator.discountedPrice(basePrice);
```
