# Javascript语法简述

### 1. 数据类型 (7种)

##### 1.1 基本数据类型
> A primitive (primitive value, primitive data type) is data that is not an object and has no methods. 
> Most of the time, a primitive value is represented directly at the lowest level of the language implementation.

* [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)  
 > undefined is a property of the global object  
 
 **动态语言中，变量没有固定的*type*，数值的变化导致选用了不同的*type*。因此当变量未赋值时，其type为`undefined`。相较静态语言中，每个变量都有固定的*type*，数值的变化是基于*type*内的。**
 ```javascript
 if (x === undefined) { // Strict equality
 }
 if (typeof x === 'undefined') { // Typeof operator, does not throw an error if not declared
 }
 ```
 
* [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)  
 > The value null is a literal (not a property of the global object like `undefined` can be).  
 > It is one of JavaScript's primitive values. (不是primitive type？)
 
 **为何不与`undefined`以相同方式实现呢？**
 ```javascript
 typeof null        // object (bug in ECMAScript, should be null)
 typeof undefined   // undefined
 null === undefined // false
 null  == undefined // true 

 ```

* [Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)  
 > Numbers in JavaScript are "double-precision 64-bit format IEEE 754 values".
 > There's no such thing as an integer in JavaScript, In practice, integer values are treated as 32-bit ints, and some implementations even store it that way (该如何理解？)
 > a built-in object [`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math) provides advanced mathematical functions and constants
 
 ```javascript
 "37" + 7 // "377", string + number
 37 + "7" // "377", string + number
 "37" - 7 // 30, string -> number
 parseInt("123", 10); // 123, string -> number
 Math.sin(3.5); // Math function
 Math.PI * (r + r); // Math constant
 ```
 
  * [NaN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN)  
   > NaN is a property of the global object.  
   
     ```javascript
     parseInt("hello", 10); // NaN
     NaN + 5; // NaN
     isNaN(NaN); // true
     ```
  
  * [Infinity](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Infinity)
   > Infinity is a property of the global object  
   > The initial value of Infinity is Number.POSITIVE_INFINITY  
   
     ```javascript
     -1 / 0; // -Infinity
     isFinite(1/0); // false
     ```
 
 [比较各语言的整数](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/01-CompareInteger)  
 [比较各语言的浮点数](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/02-CompareFloat)  

* Bool  

* String  

* Symbol  

##### 1.2 复杂数据类型

* Object  

##### 1.3 特殊数据类型

### 2. 表达式与操作符

### 3. 语句与控制

### 4. 函数

### 5. 原型

### 参考
语法参考：[A re-introduction to JavaScript (JS tutorial)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)  
进阶读物：[《JavaScript: The Good Parts》](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742)， [《JavaScript语言精粹》](http://www.amazon.cn/JavaScript%E8%AF%AD%E8%A8%80%E7%B2%BE%E7%B2%B9-%E9%81%93%E6%A0%BC%E6%8B%89%E6%96%AF%E2%80%A2%E5%85%8B%E7%BD%97%E5%85%8B%E7%A6%8F%E5%BE%B7/dp/B0097CON2S)  
Style Guide：[Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)  
