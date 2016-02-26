# Javascript语法简述

### 1. 数据类型 (7种)

##### 1.1 基本数据类型
> A primitive (primitive value, primitive data type) is data that is not an object and has no methods. 
> Most of the time, a primitive value is represented directly at the lowest level of the language implementation.

* [undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined) ([Source](https://github.com/v8/v8/blob/master/src/heap-symbols.h), [Source](https://github.com/v8/v8/blob/master/src/objects.h), [Source](https://github.com/v8/v8/blob/master/src/factory.h))  
 > undefined is a property of the global object  
 
 **动态语言中，变量没有固定的*type*，数值的变化导致选用了不同的*type*。因此当变量未赋值时，其type为`undefined`。相较静态语言中，每个变量都有固定的*type*，数值的变化是基于*type*内的。**
 ```javascript
 if (x === undefined) { // Strict equality
 }
 if (typeof x === 'undefined') { // Typeof operator, does not throw an error if not declared
 }
 ```
 
* [null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null) ([Source](https://github.com/v8/v8/blob/master/src/heap-symbols.h), [Source](https://github.com/v8/v8/blob/master/src/objects.h), [Source](https://github.com/v8/v8/blob/master/src/factory.h))  
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
 37 - "7" // 30, string -> number
 parseInt("123", 10); // 123, string -> number
 Math.sin(3.5); // Math function
 Math.PI * (r + r); // Math constant
 ```
 
  * [NaN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN)  
  * [Infinity](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Infinity)  

 [比较各语言的整数](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/01-CompareInteger)  
 [比较各语言的浮点数](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/02-CompareFloat)  

* [Bool](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)  
 > The Boolean type has two literal values: `true` and `false`. (是否说成keywords更好?)  
 > Any value can be converted to a boolean according to the following rules:  
 > 1. `false`, `0`, empty strings (""), `NaN`, `null`, and `undefined` all become false.  
 > 2. All other values become true.  

* [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)  
 > Strings in JavaScript are sequences of `Unicode characters`. Each `Unicode character` is represented by either 1 or 2 code units (UTF-16).  
 > strings like objects, they have methods as well that allow you to manipulate the string and access information about the string  
 
 ```javascript
 "hello".length; // length
 "hello".charAt(0); // accessing
 "hello, world".replace("hello", "goodbye"); // replace
 ```

* [Symbol (ES6)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)  
 > A symbol is a unique and immutable data type and may be used as an identifier for object properties.  
 
 ```javascript
 var sym1 = Symbol();
 var sym2 = Symbol("foo");
 ```

##### 1.2 复杂数据类型

* [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)  
 ```javascript
 var obj = {};
 var obj = {
    "name": "Carrot",  
    details: {
      color: "orange",
      size: 12
    }
 }
 obj.details.color; // orange
 obj["details"]["size"]; // 12
 ```
 
 * [Object.prototype](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype)  
   > All objects in JavaScript are descended from Object; all objects inherit methods and properties from Object.prototype  
   
     ```javascript
     function Person(name, age) {
       this.name = name;  
       this.age = age;
     }
     var You = new Person("You", 24); 
     ```
   
 * [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)  
   > Arrays in JavaScript are actually a special type of object.   
   > magic property `length` - one more than the *highest index* in the array.  
   
     ```javascript
     var a = ["dog", "cat", "hen"]; // init, with array literal
     a[100] = "fox"; // insert / replace
     a.push("goat"); // append, see also: pop, shift, unshift
     a.length; // 102, magic length property
     typeof a[90]; // undefined, accessing
     for (var i = 0; i < a.length; i++) { // for loop, bad, NOT preferred idiom
     }
     a.forEach(function(currentValue, index, array) { // forEach, good, NOT best choice
     });
     ```

 * [Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions)  
   > functions are the **core component** in understanding JavaScript   
   
     ```javascript
     function avg() {
       return sum / arguments.length; // arguments.length
     }
     avg.apply(null, [2, 3, 4, 5]); // apply, convert array to function parameters
     (function() {
     })();           // IIFE (Immediately Invoked Function Expressions), "hide" local variables 
     var cnt = (function counter() {
     })();           // IIFE with name, used for, e.g. recursion
     ```

 * [Date](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date)  
   > Date objects are based on a time value that is the number of milliseconds since 1 January, 1970 UTC.  
   
     ```javascript
     var today = new Date();
     var birthday = new Date('1995-12-17T03:24:00');
     var elapsed = today - birthday; // elapsed time in milliseconds
     ```

 * [RegExp](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)  
   > flags: g (global), i (ignore case), m (multiline), u (unicode), y (sticky)
   
     ```javascript
     var reg = /(\w+)\s(\w+)/; // init with literal
     var lines = text.split(/\r\n|\r|\n/); // apply
     ```

### 2. 表达式与操作符

### 3. 语句与控制

### 4. 函数

### 5. 原型

### 6. 调试相关
* 打印语句：
 ```javascript
 console.log(" ") // print
 ```

 [比较各语言的打印语句](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/91-CompareLog)  
 
* Exception (try/throw/catch)：
 
 [比较各语言的Exception Handling](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/92-CompareException)  
 
* Assertion：
 ```javascript
 ```
 
 [比较各语言的Assertion](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/93-CompareAssertion)  

### 参考
语法参考：[A re-introduction to JavaScript (JS tutorial)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/A_re-introduction_to_JavaScript)  
进阶读物：[《JavaScript: The Good Parts》](http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742)， [《JavaScript语言精粹》](http://www.amazon.cn/JavaScript%E8%AF%AD%E8%A8%80%E7%B2%BE%E7%B2%B9-%E9%81%93%E6%A0%BC%E6%8B%89%E6%96%AF%E2%80%A2%E5%85%8B%E7%BD%97%E5%85%8B%E7%A6%8F%E5%BE%B7/dp/B0097CON2S)  
装B资源：[javascript源代码(chrome v8)](https://github.com/v8/v8)  
Style Guide：[Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)  
