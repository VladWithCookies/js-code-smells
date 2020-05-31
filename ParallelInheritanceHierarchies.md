# Parallel Inheritance Hierarchies
## Reason
Whenever you create a subclass for a class, you find yourself needing to create a subclass for another class.

## Solutions
### Move Method & Move Field
```js
// Bad
class Engineer {
  //...
}

class MileStone {
  //...
}

class ComputerEngineer extends Engineer {
  //...
  setType(type) {
    this.type = type;
  }
    
  setSalary(salary) {
    this.salary = salary;
  }
    
  setMileStone(MileStone mileStone) {
    this.mileStone = mileStone;
  }
  
  getType() {
    return this.type;
  }

  getSalary() {
    return this.salary;
  }
  
  getMileStone() {
    return this.mileStone;
  }
   
  toString() {
    return `Computer engineer, type is ${this.type}, salary is ${this.salary}, mileStone is ${this.mileStone}`;
  }
}

class ComputerMileStone extends MileStone {
  work() {
    return 'Build a Billing MicroService';
  }
    
  target() {
    return 'Has to be finshed in 14 PD';
  }
  
  toString() {
    return `Computer mile stone work is ${this.work()}, target is ${this.target()}`;
  }
}

class CivilEngineer extends Engineer {
  //...
  setType(type) {
    this.type = type;
  }
    
  setSalary(salary) {
    this.salary = salary;
  }
    
  setMileStone(mileStone) {
    this.mileStone = mileStone;
  }
    
  getType() {
    return type;
  }

  getSalary() {
    return salary;
  }

  getMileStone() {
    return mileStone;
  }
       
  toString() {
    return `Civil engineer type is ${this.type}, salary is ${this.salary}, mileStone is ${this.mileStone}`;
  }
}

class CivilMileStone extends MileStone {
  work() {
    return 'Create  Twin Towers';
  }
  
  target() {
    return 'Has to be completed in 2 years';
  }
  
  toString() {
    return `Civil mile stone work is ${this.work()}, target is ${this.target()}`;
  }
}

const computerEngineer = new ComputerEngineer();

computerEngineer.setType('Computer Engineer');
computerEngineer.setSalary(50000);
computerEngineer.setMileStone(new ComputerMileStone());

const civilEngineer = new CivilEngineer();

civilEngineer.setType('Civil Engineer');
civilEngineer.setSalary(60000);
civilEngineer.setMileStone(new CivilMileStone());

//Better
class EngineerMileStone {
  //...
}

class ComputerEngineer extends EngineerMileStone {
  //...
  getType() {
    return this.type;
  }
 
  setType(type) {
    this.type = type;
  }
    
  getSalary() {
    return this.salary;
  }
  
  setSalary(salary) {
    this.salary = salary;
  }
  
  work() {
    return 'Build a Billing MicroService';
  }
  
  target() {
    return 'Has to be finshed in 14 PD';
  }
  
  toString() {
    return `Computer engineer type is `${this.type}, salary is `${this.salary}, work is ${this.work()}, target is `${this.target()}`;
  }
}

class CivilEngineer extends EngineerMileStone {
  //...
  getType() {
    return this.type;
  }
  
  setType(type) {
    this.type = type;
  }
  
  getSalary() {
    return this.salary;
  }
  
  setSalary(salary) {
    this.salary = salary;
  }
  
  work() {
    return 'Create Twin Towers';
  }
 
  target() {
    return 'Has to be completed in 2 years';
  }
  
  toString() {
    return `ReFactor civil engineer type is ${this.type}, salary is `${this.salary}, work is ${this.work()}, target is `${this.target()}`;
  }
}

const computerEngineer = new ComputerEngineer();

computerEngineer.setType("Computer Engineer");
computerEngineer.setSalary(50000);

const civilEngineer = new CivilEngineer();

civilEngineer.setType('Civil Engineer');
civilEngineer.setSalary(60000);
```
