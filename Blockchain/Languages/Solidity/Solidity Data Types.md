
# 🧮 Solidity Data Types in Blockchain Development

Solidity is a statically-typed, contract-oriented programming language designed for Ethereum and other blockchain platforms. This document explores Solidity’s key data types, their use cases, and best practices.

---

## 📜 Solidity Data Types Overview

Solidity provides a range of **value types** and **reference types**:

### **Value Types**
- **Integer (uint and int):** Fixed-size integers.
- **Boolean:** True or false values.
- **Address:** Ethereum addresses, with utility methods.
- **Fixed Point (fixed and ufixed):** Not yet fully supported.
- **Bytes:** Fixed-size byte arrays.
- **Enum:** Custom enumerations.

### **Reference Types**
- **Arrays:** Dynamic and fixed-size arrays.
- **Mapping:** Key-value pairs for storage.
- **Structs:** Custom data structures.

For more details, see [Solidity Documentation on Data Types](https://docs.soliditylang.org/en/latest/types.html).

---

## 🔢 Integers in Solidity

### **Unsigned Integers (uint)**
- **uint**: Unsigned integers (`0` to `2^256 - 1`).
- Common sizes: `uint8`, `uint16`, ..., `uint256`.

#### **Example:**
```solidity
uint8 smallNumber = 255; // 8-bit unsigned integer
uint256 largeNumber = 1234567890; // 256-bit unsigned integer
```

### **Signed Integers (int)**
- **int**: Signed integers (`-2^(n-1)` to `2^(n-1) - 1`).
- Common sizes: `int8`, `int16`, ..., `int256`.

#### **Example:**
```solidity
int8 smallInt = -128; // 8-bit signed integer
int256 largeInt = 987654321; // 256-bit signed integer
```

### **Best Practices**
- Use `uint` (alias for `uint256`) when you don't need negative values.
- Prefer smaller sizes like `uint8` for efficiency but only when appropriate.

For more, see [Optimizing Gas Costs](../Development%20Practices/Optimizing%20Gas%20Costs.md).

---

## 📜 Boolean

Booleans are used for logical operations and conditions.

### **Example:**
```solidity
bool isActive = true;
if (isActive) {
    // Execute some logic
}
```

### **Best Practices**
- Avoid multiple `bool` variables in storage due to gas inefficiency.

For gas optimization, see [Optimizing Gas Costs](../Development%20Practices/Optimizing%20Gas%20Costs.md).

---

## 🏗️ Address

The `address` type stores Ethereum addresses and includes utility methods:

### **Example:**
```solidity
address owner = 0x1234567890abcdef1234567890abcdef12345678;
```

### **Utility Methods**
- `balance`: Returns the balance of the address in WEI.
- `transfer(amount)`: Transfers ETH to the address.

#### **Example:**
```solidity
address payable recipient = payable(0x1234567890abcdef1234567890abcdef12345678);
recipient.transfer(1 ether); // Send 1 ETH
```

### **Best Practices**
- Use `address payable` for addresses involved in ETH transfers.

For more, see [Handling ETH and WEI](../Development%20Practices/Handling%20ETH%20and%20WEI.md).

---

## 🔢 Fixed-Point Numbers (Experimental)

### **Overview**
- **fixed/ufixed**: Fixed-point numbers for decimals.
- Currently not fully supported.

---

## 📦 Bytes

### **Fixed-Size Bytes**
- `bytes1` to `bytes32`: Fixed-size byte arrays.

#### **Example:**
```solidity
bytes32 hash = keccak256(abi.encodePacked("data"));
```

### **Dynamic Bytes**
- `bytes`: Dynamically-sized byte arrays.
- Use `string` for textual data.

#### **Example:**
```solidity
bytes memory dynamicData = "Hello, Blockchain!";
```

---

## 📜 Arrays

Arrays store ordered lists of elements.

### **Fixed-Size Arrays**
```solidity
uint[5] fixedArray = [1, 2, 3, 4, 5];
```

### **Dynamic Arrays**
```solidity
uint[] dynamicArray;
dynamicArray.push(10); // Add an element
```

---

## 📖 Structs

Structs allow for custom data structures.

### **Example:**
```solidity
struct Token {
    string name;
    uint256 supply;
}

Token myToken = Token("MyToken", 1000000);
```

---

## 🗺️ Mappings

Mappings store key-value pairs.

### **Example:**
```solidity
mapping(address => uint256) public balances;
balances[msg.sender] = 100;
```

---

## 🔗 Related Notes
- [Type Conversions](../Development%20Practices/Type%20Conversions.md)
- [Optimizing Gas Costs](../Development%20Practices/Optimizing%20Gas%20Costs.md)
- [Handling ETH and WEI](../Development%20Practices/Handling%20ETH%20and%20WEI.md)
