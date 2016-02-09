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

 ```swift
 let π = 3.14159
 let anotherPi = 3 + 0.14159
 ```
 
 swift中定义了`Float.infinity`和`Double.infinity`，然而并没有定义epsilon。**Style guide中也并没有关于Double、Float相等性(equality)的推荐用法**
 
 [比较各语言的浮点数]()

* Bool  
> Swift provides two Boolean constant values, `true` and `false`
> Swift’s type safety prevents non-Boolean values from being substituted for `Bool`.  

 ```swift
 let i = 1
 if i == 1 { // 不能写作 if i {
 }
 ```
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
> Tuples group multiple values into a single compound value. The values within a tuple can be of any type and do not have to be of the same type as each other.  
> Tuples are particularly useful as the return values of functions.  
 
 ```swift
 let http404Error = (404, "Not Found")
 ```

* Optionals  
> You use optionals in situations where a value may be absent.  

 ```swift
 var surveyAnswer: String? // surveyAnswer is automatically set to nil
 ```
 * Optional Binding  
   
   > You can include multiple optional bindings in a single if statement and use a where clause to check for a Boolean condition  
   
     ```swift
     let possibleNumber = "123"
     if let actualNumber = Int(possibleNumber) {
     }
     ```
 
 * Implicitly Unwrapped Optionals  
   
   > Sometimes it is clear from a program’s structure that an optional will always have a value, after that value is first set.  
   
     **本人觉得，除了项目自动生成的Implicitly Unwrapped Optionals，如IBOutlet，应该尽量避免使用这个东东**  
     
     ```swift
     let assumedString: String! = "An implicitly unwrapped optional string."
     ```

### 2. 表达式与操作符
* let定义常量：
```swift
let π = 3.14159
```

* var定义变量：
```swift
var friendlyWelcome = "Hello!"
```

### 3. 语句与控制


### 4. 函数

### 5. 数值类型(如Structure)

### 6. 引用类型(如Class)

### 7. 调试相关
* 打印语句：
 ```swift
 print("log: " + str + \(a))
 ```

 [比较各语言的打印语句]()
 
* Exception (try/throw/catch)：
 
 [比较各语言的Exception Handling]()
 
* Assertion：
 ```swift
 assert(age >= 0, "A person's age cannot be less than zero")
 ```
 
 [比较各语言的Assertion]()

### 参考
语法参考：[The Swift Programming Language](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language)  
进阶读物：暂无  
装B资源：[Swift源代码](https://github.com/apple/swift)  
Style Guide：[The Official raywenderlich.com Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)  
