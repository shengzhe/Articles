# Swift语法简述
Swift号称是语法类似于脚本语言的、**系统级静态语言**。  

### 1. 数据类型

##### 1.1 基本数据类型
* Int  
> Swift provides signed and unsigned integers in 8, 16, 32, and 64 bit forms.  
> Use the `Int` type for all general-purpose integer constants and variables in your code, even if they are known to be non-negative.  

 `UInt8.min` ~ `UInt8.max` 范围是 0 ~ 255  
 `Int.min` ~ `Int.max` 在64位机器上的范围是 -2^63 ~ 2^63  
 [比较各语言的整数]()

* Double、Float  
> `Double` represents a 64-bit floating-point number.  
> `Float` represents a 32-bit floating-point number.  
> Swift always chooses `Double` (rather than `Float`) when inferring the type of floating-point numbers.

 ```
 let π = 3.14159
 let anotherPi = 3 + 0.14159
 ```
 
 [比较各语言的浮点数]()

* Bool  
 [比较各语言的布尔值]()

* String  
 [比较各语言的字符串]()

##### 1.2 复杂数据类型
* Array  
 [比较各语言的数组]()

* Dictionary  
 [比较各语言的键值对]()

* Set  

##### 1.2 特有数据类型
* Tuples  
* Optionals  

### 2. 表达式与操作符
* let定义常量：
```
let π = 3.14159
```

* var定义变量：
```
var friendlyWelcome = "Hello!"
```



### 3. 语句与控制
打印语句：
```
print("log: " + str + \(a))
```

### 4. 函数

### 5. 数值类型(如Structure)

### 6. 引用类型(如Class)

### 参考
语法参考：[The Swift Programming Language](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language)  
进阶读物：暂无  
装B资源：[Swift源代码](https://github.com/apple/swift)  
Style Guide：[The Official raywenderlich.com Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)  
