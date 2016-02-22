# Swift语法简述
Swift号称是语法类似于脚本语言的、**系统级静态语言**。  

### 1. 数据类型

##### 1.1 基本数据类型
* Int ([Source](https://github.com/apple/swift/blob/master/stdlib/public/core/FixedPoint.swift.gyb))  
> Swift provides signed and unsigned integers in 8, 16, 32, and 64 bit forms.  
> Use the `Int` type for all general-purpose integer constants and variables in your code, even if they are known to be non-negative.  

 `UInt8.min` ~ `UInt8.max` 范围是 0 ~ 255  
 `Int.min` ~ `Int.max` 在64位机器上的范围是 -2^63 ~ 2^63  
 [比较各语言的整数](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/01-CompareInteger)  

* Double、Float ([Source](https://github.com/apple/swift/blob/master/stdlib/public/core/FloatingPoint.swift.gyb))  
> `Double` represents a 64-bit floating-point number.  
> `Float` represents a 32-bit floating-point number.  
> Swift always chooses `Double` (rather than `Float`) when inferring the type of floating-point numbers.

 ```swift
 let π = 3.14159 // inferred as Double
 let anotherPi = 3 + 0.14159 // inferred as Double
 ```
 
 swift中定义了`Float.infinity`和`Double.infinity`，然而并没有定义epsilon。**Style guide中也并没有关于Double、Float相等性(equality)的推荐用法**
 
 [比较各语言的浮点数](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/02-CompareFloat)  

* Bool ([Source](https://github.com/apple/swift/blob/master/stdlib/public/core/Bool.swift))  
> Swift provides two Boolean constant values, `true` and `false`  
> Swift’s type safety prevents non-Boolean values from being substituted for `Bool`.  

 ```swift
 let i = 1
 if i == 1 { // 不能写作 if i {
 }
 ```
 [比较各语言的布尔值](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/03-CompareBool)  

* String (value type, pass-by-value) ([Source](https://github.com/apple/swift/blob/master/stdlib/public/core/String.swift))  
> Swift’s String type is a value type. // String在Swift中是以Struct实现的  
> Swift’s copy-by-default String behavior... Behind the scenes, Swift’s compiler optimizes string usage so that actual copying takes place only when absolutely necessary.  

 ```swift
 let someString = "Some string literal value" // initialize, from string literal
 if someString.isEmpty { // isEmpty
 }
 for character in someString.characters { // access Characters
 }
 if someString.characters.count { // characters.count
 }
 let message = "\(multiplier) times 2.5 is \(multiplier * 2.5)" // string interpolation
 ```
 
 * Unicode  
 *ignore for the moment*  
 
 * Accessing and Modifying a String  
   > Each String value has an associated index type, String.Index, which corresponds to the position of each Character in the string. 
   You can use subscript syntax to access the Character at a particular String index.  
   
     **Index 的设计糟糕透顶，以后肯定会改**
     swift2.1版本，subscript仅能用来读取Character，不能用于写入Character。弱爆了！
     ```swift
     var greeting = "Guten Tag"
     greeting[greeting.startIndex] // accessing, through Index
     greeting[greeting.startIndex.advancedBy(7)] // accessing, through Index
     greeting.insert("!", atIndex: greeting.endIndex) // insert
     greeting.removeAtIndex(greeting.endIndex.predecessor()) // remove
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
* Array (special value type, pass-by-value) ([Source](https://github.com/apple/swift/blob/master/stdlib/public/core/Arrays.swift.gyb))  
> Arrays, sets, and dictionaries in Swift are always clear about the types of values and keys that they can store.  
> Copying only takes place when you perform an action that has the potential to modify the length of the array. Array是特殊的value type.  

 不愧是强类型，但是运行时是否会因为插入不匹配的数据类型而崩溃呢？Bridge到Obj-C出现AnyObject时得额外注意这点  
 
 ```swift
 var someInts = [Int]() // initialize, empty array
 let threeDoubles = [Double](count: 3, repeatedValue: 0.0) // initialize
 var shoppingList = ["Eggs", "Milk"] // initialize, with array literal
 if shoppingList.isEmpty { // isEmpty
 }
 if shoppingList.count > 1 { // count
 }
 ```
 
 * Accessing and Modifying an Array  
 > You access and modify an array through its methods and properties, or by using subscript syntax.  
   
     ```swift
     shoppingList.append("Flour") // append
     shoppingList += ["Baking Powder"] // append, with +
     let firstItem = shoppingList[0] // accessing, throught subscript
     shoppingList[0] = "Six eggs" // replace, note: won't modify `firstItem`
     shoppingList[0...3] = ["Bananas", "Apples"] // replace range, note: with different size of items
     shoppingList.insert("Maple Syrup", atIndex: 0) // insert
     shoppingList.removeAtIndex(0) // remove
     if shoppingList.contains("Milk") {
     }
     ```
 
 * Iterating Over an Array  
     ```swift
     for item in shoppingList { // for-in loop
     }
     for (index, value) in shoppingList.enumerate() { // enumerate() 
     }
     ```
 [比较各语言的数组](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/11-CompareArray)  

* Dictionary (value type, pass-by-value) ([Source](https://github.com/apple/swift/blob/master/stdlib/public/core/HashedCollections.swift.gyb))  
> Arrays, sets, and dictionaries in Swift are always clear about the types of values and keys that they can store.  
> All of Swift’s basic types (such as String, Int, Double, and Bool) are hashable by default, and can be used as set value types or dictionary key types.  

 不愧是强类型，但是运行时是否会因为插入不匹配的数据类型而崩溃呢？Bridge到Obj-C出现AnyObject时得额外注意这点  
 
 ```swift
 var namesOfIntegers = [Int: String]() // initialize, empty array
 var airports = ["YYZ": "Toronto Pearson", "DUB": "Dublin"] // initialize, with dictionary literal
 if airports.isEmpty { // isEmpty
 }
 if airports.count > 1 { // count
 }
 ```
 
 * Accessing and Modifying a Dictionary    
 > You access and modify an array through its methods and properties, or by using subscript syntax.  
   
     ```swift
     airports["LHR"] = "London" // insert or replace, through subscript
     if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") { // return old, if replace happens
     }
     if let airportName = airports["DUB"] { // accessing, through subscript
     }
     airports["APL"] = nil // remove
     if let removedValue = airports.removeValueForKey("DUB") { // return old, when remove
     }
     ```
 
 * Iterating Over a Dictionary  
     ```swift
     for (airportCode, airportName) in airports { // for-in loop
     }
     for airportCode in airports.keys { { // loop through keys, or airports.values to loop through values
     }
     let airportCodes = [String](airports.keys) // 这个必然需要改一改
     ```
 [比较各语言的键值对](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/12-CompareDictionary)  

* Set (value type, pass-by-value) ([Source](https://github.com/apple/swift/blob/master/stdlib/public/core/HashedCollections.swift.gyb))  
> Arrays, sets, and dictionaries in Swift are always clear about the types of values and keys that they can store.  
> All of Swift’s basic types (such as String, Int, Double, and Bool) are hashable by default, and can be used as set value types or dictionary key types.  
 
 ```swift
 var letters = Set<Character>() // initialize, empty set
 var favoriteGenres: Set = ["Rock", "Classical", "Hip hop"] // initialize, with literal
 if favoriteGenres.isEmpty { // isEmpty
 }
 if favoriteGenres.count > 1 { // count
 }
 ```
 * Accessing and Modifying a Set  
 > You access and modify a set through its methods and properties.  
   
     ```swift
     favoriteGenres.insert("Jazz") // insert
     favoriteGenres.remove("Rock") // remove
     if favoriteGenres.contains("Funk") {
     }
     ```
 
 * Iterating Over a Set  
     ```swift
     for genre in favoriteGenres { // for-in loop
     }
     for genre in favoriteGenres.sort() { // loop with sort
     }
     ```
 
 * Fundamental Set Operations, Membership and Equality  
     ```swift
     a.intersect(b) // exclusiveOr(), union(), substract()
     if a == b {}
     if a.isSubsetOf(b) {} // a.isStrictSubsetOf(b)
     if a.isSupersetOf(b) {} // a.isStrictSupersetOf(b)
     if a.isDisjointWith(b) {}
     ```

##### 1.2 特有数据类型
* Tuples    
> Tuples group multiple values into a single compound value. The values within a tuple can be of any type and do not have to be of the same type as each other.  
> Tuples are particularly useful as the return values of functions.  
 
 ```swift
 let http404Error = (404, "Not Found") // tuple
 ```

* Optionals ([Source](https://github.com/apple/swift/blob/master/stdlib/public/core/Optional.swift))  
> You use optionals in situations where a value may be absent.  

 ```swift
 var surveyAnswer: String? // surveyAnswer is automatically set to nil
 ```
 * Optional Binding  
   
   > You can include multiple optional bindings in a single if statement and use a where clause to check for a Boolean condition  
   
     ```swift
     let possibleNumber = "123"
     if let actualNumber = Int(possibleNumber) { // optional, return value of func Int(String) -> Int?
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
let π = 3.14159 // let
```

* var定义变量：
```swift
var friendlyWelcome = "Hello!" // var
```

### 3. 语句与控制


### 4. 函数

### 5. 数值类型(如Structure)

### 6. 引用类型(如Class)

### 7. 调试相关
* 打印语句：
 ```swift
 print("log: " + str + \(a)) // print
 ```

 [比较各语言的打印语句](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/91-CompareLog)  
 
* Exception (try/throw/catch)：
 
 [比较各语言的Exception Handling](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/92-CompareException)  
 
* Assertion：
 ```swift
 assert(age >= 0, "A person's age cannot be less than zero") // assert
 ```
 
 [比较各语言的Assertion](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/93-CompareAssertion)  

### 参考
语法参考：[The Swift Programming Language](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/Swift_Programming_Language)  
进阶读物：暂无  
装B资源：[Swift源代码](https://github.com/apple/swift)  
Style Guide：[The Official raywenderlich.com Swift Style Guide](https://github.com/raywenderlich/swift-style-guide)  
