# Ruby语法简述

### 1. 数据类型

##### 1.1 基本数据类型  
> everything in Ruby is an object - Ruby中没有primitive data types

##### 1.2 复杂数据类型  
* Hashes  
 > Hashes are like dictionaries, in a sense.  
 
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
 
* Array
 > Arrays are a lot like Hashes, except that the keys are always consecutive numbers, and always starts at 0.  
 
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

### 参考
语法参考：[Ruby Programming - wikibooks](https://en.wikibooks.org/wiki/Ruby_Programming)  
进阶读物：[《Metaprogramming Ruby 2: Program Like the Ruby Pros》](http://www.amazon.com/Metaprogramming-Ruby-Program-Like-Facets/dp/1941222129)， [《Ruby元编程》](http://www.amazon.cn/Ruby%E5%85%83%E7%BC%96%E7%A8%8B-Paolo-Perrotta/dp/B013QMKP80)  
装B资源：[Ruby源代码](https://github.com/ruby/ruby)  
Style Guide：[Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide)， [Rails Style Guide](https://github.com/bbatsov/rails-style-guide)  
