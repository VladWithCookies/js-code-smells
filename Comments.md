# Comments
## Reason
Comments are usually created with the best of intentions, when the author realizes that his or her code isn’t intuitive or obvious. In such cases, comments are like a deodorant masking the smell of fishy code that could be improved.

## Solutions
### Extract Varialbe
```js
// Bad
renderBanner() {
  // Comment
  if ((platform.toUpperCase().indexOf("MAC") > -1) &&
       (browser.toUpperCase().indexOf("IE") > -1) &&
        wasInitialized() && resize > 0 )
  {
    //...
  }
}

// Better
renderBanner() {
  const isMacOs = platform.toUpperCase().indexOf("MAC") > -1;
  const isIE = browser.toUpperCase().indexOf("IE") > -1;
  const wasResized = resize > 0;

  if (isMacOs && isIE && wasInitialized() && wasResized) {
    //...
  }
}
```

### Extract Method
```js
// Bad
printOwing() {
  printBanner();

  // Print details.
  console.log("name: " + name);
  console.log("amount: " + getOutstanding());
}

// Better
printOwing() {
  printBanner();
  printDetails(getOutstanding());
}

printDetails(outstanding) {
  console.log("name: " + name);
  console.log("amount: " + outstanding);
}
```

### Introduce Assertion
```js
// Bad
getExpenseLimit() {
  // Should have either expense limit or a primary project.
  return (expenseLimit != NULL_EXPENSE) ? expenseLimit : primaryProject.getMemberExpenseLimit();
}

// Better
getExpenseLimit() {
  if (!expenseLimit && !primaryProject) {
    throw 'Should have either expense limit or a primary project.'
  }

  return (expenseLimit != NULL_EXPENSE) ? expenseLimit : primaryProject.getMemberExpenseLimit();
}
```
