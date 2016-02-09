# Swift语法简述
Swift号称是语法类似于脚本语言的、**系统级静态语言**。  

### 1. 数据类型

##### 1.1 基本数据类型
* Int  
> Swift provides signed and unsigned integers in 8, 16, 32, and 64 bit forms.  
> Use the `Int` type for all general-purpose integer constants and variables in your code, even if they are known to be non-negative.  

 `UInt8.min` ~ `UInt8.max` 范围是 0 ~ 255  
 `Int.min` ~ `Int.max` 在64位机器上的范围是 -2^63 ~ 2^63  
 [比较各语言的整数](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/01-CompareInteger)  

* Double、Float  
> `Double` represents a 64-bit floating-point number.  
> `Float` represents a 32-bit floating-point number.  
> Swift always chooses `Double` (rather than `Float`) when inferring the type of floating-point numbers.

 ```swift
 let π = 3.14159
 let anotherPi = 3 + 0.14159
 ```
 
 swift中定义了`Float.infinity`和`Double.infinity`，然而并没有定义epsilon。**Style guide中也并没有关于Double、Float相等性(equality)的推荐用法**
 
 [比较各语言的浮点数](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/02-CompareFloat)  

* Bool  
> Swift provides two Boolean constant values, `true` and `false`  
> Swift’s type safety prevents non-Boolean values from being substituted for `Bool`.  

 ```swift
 let i = 1
 if i == 1 { // 不能写作 if i {
 }
 ```
 [比较各语言的布尔值](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/03-CompareBool)  

* String  
> Swift’s String type is a value type. // String在Swift中是以Struct实现的  
> Swift’s copy-by-default String behavior... Behind the scenes, Swift’s compiler optimizes string usage so that actual copying takes place only when absolutely necessary.  

 ```swift
 let someString = "Some string literal value" 
 if someString.isEmpty {
 }
 for character in someString.characters { // access Characters
 }
 let message = "\(multiplier) times 2.5 is \(multiplier * 2.5)" // string interpolation
 ```
 
 * Unicode  
 *ignore for the moment*  
 
 * Accessing and Modifying a String  
   > Each String value has an associated index type, String.Index, which corresponds to the position of each Character in the string. 
   
     **Index 的设计糟糕透顶，以后肯定会改**
     ```swift
     let greeting = "Guten Tag"
     greeting[greeting.startIndex] // G
     greeting[greeting.startIndex.advancedBy(7)] // a
     greeting.insert("!", atIndex: greeting.endIndex)
     greeting.removeAtIndex(greeting.endIndex.predecessor())
     ```
 * Compare Strings  
   > String and character equality is checked with the “equal to” operator (==) and the “not equal to” operator (!=)  
   > Two String values (or two Character values) are considered equal if their extended grapheme clusters are canonically equivalent. 
   
     这种说法好高端，意思是说也许byte不一样，但是语义和读写是一样的，也相等。很合理。  
     ```swift
     if stringA == stringB { // or !=
     }
     if stringA.hasPrevix(stringB) { // or hasSuffix
     }
     ```
 
 [比较各语言的字符串](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/04-CompareString)  

##### 1.2 复杂数据类型
* Array  
 [比较各语言的数组](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/11-CompareArray)  

* Dictionary  
 [比较各语言的键值对](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/12-CompareDictionary)  

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

 [比较各语言的打印语句](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/91-CompareLog)  
 
* Exception (try/throw/catch)：
 
 [比较各语言的Exception Handling](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/92-CompareException)  
 
* Assertion：
 ```swift
 assert(age >= 0, "A person's age cannot be less than zero")
 ```
 
 [比较各语言的Assertion](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/93-CompareAssertion)  

### 参考
语法参考：[The Swift Programming Language](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language)  
进阶读物：暂无  
装B资源：[Swift源代码](https://github.com/apple/swift)  
Style Guide：[The Official raywenderlich.com Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)  
