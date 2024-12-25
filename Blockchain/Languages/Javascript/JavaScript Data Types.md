
# 🧮 JavaScript Data Types in Blockchain Development

JavaScript plays a vital role in blockchain development, especially when interacting with smart contracts, handling on-chain data, and performing calculations. This document explores the key JavaScript data types you’ll encounter and their use cases in blockchain.

---

## 📜 JavaScript’s Core Data Types

JavaScript has several data types, broadly divided into **primitive** and **non-primitive** categories.

### Primitive Data Types

1. **String**: Represents textual data (e.g., `"Hello, world!"`).
2. **Number**: Represents numeric values (both integers and floating-point).
3. **BigInt**: For arbitrarily large integers.
4. **Boolean**: True or false values.
5. **Null**: Represents an intentional absence of value.
6. **Undefined**: Represents an uninitialized variable.
7. **Symbol**: Unique identifiers.

### Non-Primitive Data Types

- **Object**: A collection of key-value pairs, including arrays, functions, and more.

For a detailed guide on JavaScript data types, visit [MDN’s JavaScript Data Types](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures).

---

## 🔢 Numbers in JavaScript

### Floating-Point Precision
JavaScript numbers use the IEEE 754 standard for 64-bit floating-point representation. This allows for a wide range of values but introduces **precision issues** for large integers or very small decimals.

#### **Example of Precision Loss**
```javascript
const num = 12345678901234567890;
console.log(num); // 12345678901234567000 (Precision loss)
```

### Safe Integer Range
Numbers in JavaScript are **safe** up to `2^53 - 1` (`Number.MAX_SAFE_INTEGER`):
```javascript
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991
console.log(Number.MIN_SAFE_INTEGER); // -9007199254740991
```

For values beyond this range, use [BigInt](#-bigint-in-javascript).

---

## 🔢 BigInt in JavaScript

### What is BigInt?
Introduced in ES2020, `BigInt` allows you to represent integers of **arbitrary size** without precision loss.

### **Use Cases in Blockchain**
- Storing large numbers like **WEI** (smallest unit of ETH).
- Performing arithmetic on balances or token supplies.

#### **Example: Creating BigInts**
```javascript
const largeNumber = BigInt("123456789012345678901234567890");
const anotherBigInt = 12345678901234567890n; // Using the `n` suffix
```

### **BigInt Arithmetic**
BigInts support basic operations but cannot mix with `number`:
```javascript
const a = BigInt(10);
const b = BigInt(20);
console.log(a + b); // 30n

// Mixing BigInt and Number throws an error:
console.log(a + 10); // TypeError
```

For more on BigInt, see [MDN BigInt Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt).

---

## 📜 Strings in Blockchain Development

Strings are essential for **human-readable data** in blockchain development.

### **Use Cases**
- Representing addresses (`"0x1234..."`).
- Displaying balances or metadata (e.g., `"Token Name"`).

### **String to Number Conversion**
To parse strings into numbers:
```javascript
const str = "12345.67";
const num = parseFloat(str);
console.log(num); // 12345.67
```

For converting to BigInt, see [BigInt in JavaScript](#-bigint-in-javascript).

---

## 🔀 Type Conversions in Blockchain

Blockchain applications often involve conversions between strings, numbers, and BigInts.

### String → Number
Use `parseFloat` for floating-point or `parseInt` for integers:
```javascript
const str = "12345";
const num = parseInt(str);
```

### String → BigInt
Use `BigInt`:
```javascript
const bigInt = BigInt("12345");
```

### Number → BigInt
Convert integers with `BigInt`:
```javascript
const num = 12345;
const bigInt = BigInt(num);
```

For more conversion examples, see [Type Conversions in Blockchain](./Type%20Conversions.md).

---

## 💱 ETH and WEI in JavaScript

### Overview
- **WEI**: Smallest unit of ETH.
- **ETH**: Human-readable denomination.

### Conversions
Using `ethers.js`, you can safely convert between ETH and WEI:
```javascript
const wei = ethers.utils.parseEther("1.5"); // Converts 1.5 ETH to WEI
const eth = ethers.utils.formatEther("1500000000000000000"); // Converts WEI to ETH
```

For a detailed guide, see [Handling ETH and WEI](./Handling%20ETH%20and%20WEI.md).

---

## 🛑 Common Pitfalls

### Precision Loss with Numbers
Large integers and small decimals can lose precision:
```javascript
const smallDecimal = 0.000000123;
console.log(smallDecimal.toString()); // "1.23e-7"
```

### Mixing BigInt and Number
Avoid combining `BigInt` with `number`:
```javascript
const bigInt = BigInt(10);
const num = 10;
console.log(bigInt + num); // TypeError
```

For solutions, see [BigInt Operations](./BigInt%20Operations.md).

---

## 🔗 Related Notes
- [Type Conversions](./Type%20Conversions.md)
- [BigInt Operations](./BigInt%20Operations.md)
- [Handling ETH and WEI](./Handling%20ETH%20and%20WEI.md)
- [Solidity Data Types](../Solidity/Solidity%20Data%20Types.md)
