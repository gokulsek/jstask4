

## SECTION 1 – Real-Time Function Logic

### 1. Payroll System

```js
function calculateSalary(basicSalary, bonusPercentage) {
  const bonus = basicSalary * (bonusPercentage / 100);
  const grossSalary = basicSalary + bonus;
  const tax = grossSalary * 0.05;
  const finalSalary = grossSalary - tax;

  console.log("Salary Breakdown");
  console.log("Basic Salary:", basicSalary);
  console.log("Bonus:", bonus);
  console.log("Tax (5%):", tax);
  console.log("Final Salary:", finalSalary);

  return finalSalary;
}

// Example
calculateSalary(30000, 10);
```

---

### 2. Student Result System

```js
function generateResult(name, marksArray) {
  const total = marksArray.reduce((sum, m) => sum + m, 0);
  const average = total / marksArray.length;

  let grade;
  if (average >= 80) grade = "A";
  else if (average >= 60) grade = "B";
  else if (average >= 40) grade = "C";
  else grade = "Fail";

  return {
    name,
    total,
    average,
    grade
  };
}

// Example
console.log(generateResult("Rahul", [70, 80, 90]));
```

---

## SECTION 2 – Scope & Hoisting (Debugging)

### 3. Debug This Code

```js
function demo() {
  if (true) {
    var a = 10;
    let b = 20;
  }
  console.log(a);
  console.log(b);
}
demo();
```

#### What will happen?

* `10` will print
* `ReferenceError: b is not defined`

#### Why?

* `var` is **function-scoped**
* `let` is **block-scoped**

#### Fixed Code

```js
function demo() {
  let a, b;
  if (true) {
    a = 10;
    b = 20;
  }
  console.log(a);
  console.log(b);
}
demo();
```

---

### 4. Hoisting Analysis

```js
console.log(x);
var x = 100;

console.log(y);
let y = 200;
```

#### Output

```js
undefined
ReferenceError: Cannot access 'y' before initialization
```

#### Explanation

* `var` is hoisted and initialized as `undefined`
* `let` is hoisted but stays in **Temporal Dead Zone**

---

## SECTION 3 – Callback & Higher Order Functions

### 5. Order Processing System

```js
function generateInvoice(orderId) {
  console.log(`Invoice generated for Order ${orderId}`);
}

function processOrder(orderId, callback) {
  console.log("Order Processed");
  callback(orderId);
}

// Example
processOrder(101, generateInvoice);
```

---

### 6. Bank Transaction System

```js
let balance = 1000;

function sendSMS(msg) {
  console.log("SMS:", msg);
}

function transaction(amount, type, callback) {
  if (type === "deposit") balance += amount;
  else if (type === "withdraw") balance -= amount;

  callback(`Transaction successful. Balance: ${balance}`);
}

// Example
transaction(500, "deposit", sendSMS);
```

---

## SECTION 4 – Currying (E-Commerce)

### 7. Dynamic Price Builder

```js
const priceBuilder = basePrice => discount => tax => {
  const discountedPrice = basePrice - (basePrice * discount / 100);
  const finalPrice = discountedPrice + (discountedPrice * tax / 100);
  return finalPrice;
};

// Example
console.log(priceBuilder(2000)(15)(18));
```

---

## SECTION 5 – IIFE (Security + Encapsulation)

### 8. Secure Company Module

```js
const companyModule = (function () {
  const companyCode = "COMP-789"; // private

  return {
    getCompanyStatus() {
      return `Company is active with code ${companyCode}`;
    }
  };
})();

console.log(companyModule.getCompanyStatus());
// console.log(companyCode);  Not accessible
```

---

## SECTION 6 – Generator (Advanced Logic)

### 9. Unique Order ID Generator

```js
function* orderIdGenerator() {
  let id = 1000;
  while (true) {
    yield `ORD${++id}`;
  }
}

const orderGen = orderIdGenerator();
console.log(orderGen.next().value);
console.log(orderGen.next().value);
console.log(orderGen.next().value);
```

---

### 10. Coupon Spin System

```js
function* couponGenerator() {
  yield "10% OFF";
  yield "20% OFF";
  yield "50% OFF";
  yield "No Luck";
  yield "Jackpot";
}

const spin = couponGenerator();
console.log(spin.next().value);
console.log(spin.next().value);
console.log(spin.next().value);
console.log(spin.next().value);
console.log(spin.next().value);
```

---

## SECTION 7 – Mini Project (Integrated)

```js
const shop = (function () {
  let cart = [];

  function addToCart(product, price) {
    cart.push({ product, price });
  }

  function calculateTotal() {
    return cart.reduce((sum, item) => sum + item.price, 0);
  }

  const applyDiscount = total => discount => total - (total * discount / 100);

  function* generateCoupon() {
    yield "10% OFF";
    yield "20% OFF";
  }

  function processPayment(amount, callback) {
    console.log(`Payment of ${amount} processed`);
    callback();
  }

  return {
    addToCart,
    calculateTotal,
    applyDiscount,
    generateCoupon,
    processPayment
  };
})();

// Usage
shop.addToCart("Laptop", 50000);
shop.addToCart("Mouse", 1000);

let total = shop.calculateTotal();
total = shop.applyDiscount(total)(10);

shop.processPayment(total, () => {
  console.log("Payment Successful");
});
```

---

## CONCEPT QUESTIONS

### 1. Function Declaration vs Expression

| Declaration   | Expression            |
| ------------- | --------------------- |
| Hoisted       | Not hoisted           |
| Named         | Can be anonymous      |
| Used anywhere | Used after definition |

---

### 2. What is Higher Order Function?

A function that **accepts another function as argument or returns a function**.
Example: `map`, `filter`, `reduce`.

---

### 3. Real-Time Example of Generator

* Infinite scrolling
* Coupon systems
* Order ID generation
* Pagination

---

### 4. Why do we use IIFE?

* Data hiding
* Avoid global pollution
* Secure configuration

---

### 5. Difference between var, let, const

| Feature  | var      | let   | const |
| -------- | -------- | ----- | ----- |
| Scope    | Function | Block | Block |
| Hoisting | Yes      | TDZ   | TDZ   |
| Reassign | Yes      | Yes   | No    |
