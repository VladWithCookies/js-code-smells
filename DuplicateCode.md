# Duplicate Code
## Reason
Duplication usually occurs when multiple programmers are working on different parts of the same program at the same time. Since they’re working on different tasks, they may be unaware their colleague has already written similar code that could be repurposed for their own needs.

## Solutions
### Extract Superclass
```js
// Bad
class Tank {
  getHealth() {
    //...
  }
}

class Soilder { 
  getHealth() {
    //...
  }
}

// Better
class Unit {
  getHealth() {
    //...
  }
}

class Tank extends Unit {
  //...
}

class Soilder extends Unit { 
  //...
}
```

### Pull Up Field
```js
// Bad
class Unit {
  //...
}

class Tank extends Unit {
  getHealth() {
    //...
  }
}

class Soilder extends Unit { 
  getHealth() {
    //...
  }
}

// Better
class Unit {
  getHealth() {
    //...
  }
}

class Tank extends Unit {
  //...
}

class Soilder extends Unit { 
  //...
}
```

### Pull Up Constructor Body
```js
// Bad
class Employee {
  //...
}

class Manager extends Employee {
  constructor(name: string, id: string, grade: number) {
    this.name = name;
    this.id = id;
    this.grade = grade;
  }
  // ...
}

// Better
class Employee {
  constructor(name: string, id: string) {
    this.name = name;
    this.id = id;
  }
  // ...
}

class Manager extends Employee {
  constructor(name: string, id: string, grade: number) {
    super(name, id);
    this.grade = grade;
  }
  // ...
}
```
