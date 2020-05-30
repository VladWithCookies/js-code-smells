# Primitive Obsession
## Reason 
Like most other smells, primitive obsessions are born in moments of weakness. “Just a field for storing some data!” the programmer said. Creating a primitive field is so much easier than making a whole new class, right? And so it was done. Then another field was needed and added in the same way. Lo and behold, the class became huge and unwieldy.
Primitives are often used to “simulate” types. So instead of a separate data type, you have a set of numbers or strings that form the list of allowable values for some entity. Easy-to-understand names are then given to these specific numbers and strings via constants, which is why they’re spread wide and far.

## Solutions
### Replace Data Value with Object

```js
// Bad
class Order {
  customerName ='General Kenobi'
  customerEmail = 'kenobi@test.io'
}

// Better
class Order {
   constrictor() {
      this.customer = new Customer();
   }
}

class Customer {
  name = 'General Kenobi'
  email = 'kenobi@test.io'
}
```
