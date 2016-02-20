# Ruby语法简述

### 1. 数据类型

##### 1.1 基本数据类型  
> everything in Ruby is an object - Ruby中没有primitive data types

##### 1.2 复杂数据类型  
* Numbers [Fixnum](http://ruby-doc.org/core-2.3.0/Fixnum.html) & [Bignum](http://ruby-doc.org/core-2.3.0/Bignum.html) & [Float](http://ruby-doc.org/core-2.3.0/Float.html)  
 > Integers can be any length (up to a maximum determined by the amount of free memory on your system)  
 > `Fixnum` holds Integer values that can be represented in a native machine word (minus 1 bit).  
 > `Bignum` objects are created automatically when integer calculations would otherwise overflow a `Fixnum`  
 > Float objects represent inexact real numbers using the native architecture's double-precision floating point representation.  
 
 ```ruby
 10.times {|number| puts number} # loop, print 0 ~ 9
 1.upto(10) {|number| puts "#{number} Ruby loops"} # loop, 1 ~ 10
 5.step(50, 5) {|x| puts x} # loop, with step
 451.to_s # to_s, 3.1415926.to_s
 5.6.to_i # to_i
 5.to_f # to_f
 ```
 
* [Strings](http://ruby-doc.org/core-2.3.0/String.html)   
 > A String object holds and manipulates an arbitrary sequence of bytes, typically representing characters.
 > (OptionA) Prefer single-quoted strings when you don't need string interpolation or special symbols.   
 > (OptionB) Prefer double-quotes unless your string literal contains " or escape characters you want to suppress.  
 
 ```ruby
 name = 'Bozhidar' # string literal
 %(<tr><td class="name">#{name}</td>) # single-line strings with interpolation and embedded double-quotes
 'C'.ord # ASCII, inverse of 67.chr
 'Iterate'.chars # characters
 'concatenated ' + 'string!' # concat, NOT preferred as interpolation
 'Hello'.scan(/./) {|letter| puts letter} # iterate (regexp in scan)
 puts 'found number' if 'C3-P0' =~ /[0-9]/ # compare with regexp (=~)
 'Hi'.sub('i', "ello") # substitute/replace, or `tr` 
 ```
 
* [Hash](http://ruby-doc.org/core-2.3.0/Hash.html)  
 > A Hash is a dictionary-like collection of unique keys and their values.   
 
 ```ruby
 hash = {} # init
 hash = { one: 1, two: 2, three: 3 } # init (:one => 1 is bad)
 hash.size # alias of length (Enumerable#count is bad for performance)
 hash[:test] = 0 # insert / replace
 hash.key?(:test) # check key
 hash.fetch(:test, 0) # introduce default values (hash[:test] || 0, custom logic is bad)
 hash.each_value { |v| p v } # iterate keys/values
 hash.each do |key, value| # iterate, do...end for multi line block
 end
 hash.delete(:test) # remove
 hash.delete_if {|key, value| value == 0} # conditional remove, {...} for single line block
 ```
 
* [Array](http://ruby-doc.org/core-2.3.0/Array.html)  
 > Arrays are ordered, integer-indexed collections of any object.  
 
 ```ruby
 array2 = [] # init
 array = ["hello", "this", "is", "an", "array!"] # init
 array << "haha" # push
 array2 << array.pop until array.empty? # pop
 array2 = array - ["haha"] # substract
 array2 = array + ["hehe"] # union
 string = array.join(" ") # array to string
 ```
 
##### 1.3 其它数据类型  
* Constants  
 > Constants start with capital letters.  
 
 ```ruby
 SOME_CONST = 5 # define (SomeConst is bad)
 ```
 
* Symbols  
 > Symbols are lightweight objects best used for comparisons and internal logic.  

 

### 2. 表达式与操作符

### 3. 语句与控制

### 4. 函数

### 5. 类

### 6. 调试相关
* 打印语句：
 ```ruby
 puts " " # print with newline
 ```

 [比较各语言的打印语句](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/91-CompareLog)  
 
* Exception (try/throw/catch)：
 
 [比较各语言的Exception Handling](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/92-CompareException)  
 
* Assertion：
 ```ruby
 ```
 
 [比较各语言的Assertion](https://github.com/shengzhe/Articles/tree/master/LanguagesCompare/CompareSyntax/93-CompareAssertion)  


### 参考
语法参考：[Ruby Programming - wikibooks](https://en.wikibooks.org/wiki/Ruby_Programming)  
进阶读物：[《Metaprogramming Ruby 2: Program Like the Ruby Pros》](http://www.amazon.com/Metaprogramming-Ruby-Program-Like-Facets/dp/1941222129)， [《Ruby元编程》](http://www.amazon.cn/Ruby%E5%85%83%E7%BC%96%E7%A8%8B-Paolo-Perrotta/dp/B013QMKP80)  
装B资源：[Ruby源代码](https://github.com/ruby/ruby)  
Style Guide：[Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide)， [Rails Style Guide](https://github.com/bbatsov/rails-style-guide)  
