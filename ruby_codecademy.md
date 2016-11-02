**Ruby**

Three data types:

+ Number

+ String

+ Boolean

---

Declaring variables in `Ruby`:

```
my_num = 100
```

Variables in ruby have conditional assignment operator `||=`. This will assign a value to
a variable if it does not already have one.

To log something to console, use `puts` and `print`

```
puts "Hello"
print "Hello yourself"
```

`puts` adds a new line after printing to console

---

Everything in ruby is an `object`. Methods on `objects` are invoked with a `.`

```
#this is a comment
"Vamsi".length #this is a comment
"Vamsi".reverse
"vamsi".upcase
"VAMSI".downcase
```

> you do not need paranthesis after a method to invoke it.

This is a `multiline` comment:

```
=begin
This is a 
multiline
comment.
=end
```

> variables must be declared using lowercase characters separated by `underscores`. Local variables, must by convention not use a `$` or a `@`

To write multiline statements on a single line, use the `;`:

```
def no_op; end
```

Methods can be chained like:

```
name = "vamsi"
name.downcase.reverse.upcase
```

Ruby uses `gets` to recieve input,`chomp` removes the extra line after the input. For String Interpolation Ruby uses the `#{variableName}` syntax within regular strings.

To mutate a variable without writing an explicit assignment statement, use the `!` at the end of the method:

```
first_name.capitalize!
state.upcase!
```

---

Ruby does not care about whitespace in control-flow statement, the indentation is just a convention followed by Ruby programmers.

```
if expression
	Statement
else
	Statement
end
```

`unless` checks if an expression is false instead of checking if an expression is true:

```
unless expression
	puts "Works only when expression is falsy"
else
	puts "Works only when expression is truthy"
end
```

There are also simpler versions of the `if` and `unless` statements that can be written on a single line.

```
puts "It's real" if true
puts "It's really real" unless not_really_real
```

Ruby also includes a ternary operator:

```
puts 2.5 > 3.5 ? "Not printed": "Printed"
```

Ruby also provides a switch/case statement:

```
case greeting
	when "English"
		#code
		#code
	end
	else
		#this is the default case
	end
end
```

or a simpler one-liner `case` statments:

```
case greeting
    when "English" then puts "Hello!"
    when "French" then puts "Bonjour!"
    when "German" then puts "Guten Tag!"
    when "Finnish" then puts "Haloo!"
    else puts "I don't know that language"
end
```

`while` in Ruby looks like this:

```
i = 1
while i < 10
	puts i
	i = i + 1
end
```

Ruby has an `until` loop which repeats the body when the expression is `false`

```
i = 0
until i == 6
	i = i + 1
end
puts i
```

Ruby has for loops:

```
for num in 1..10
	puts num
end
```

Ruby also has a `loop` iterator that works like this:

```
i = 30
loop do
  i = i -1
  #skips the current iteration of the loop if number is odd
  next if i%2 == 1
  print i
  #exits the loop if the value is not a natural number
  break if i <= 0
```

Ruby has ranges for values:

`1...10` excludes the upper limit of the range

`1..10` includes the upper limit of the range

Ruby has the following standard comparision operators:

|Operator|Symbol|
|:------:|:----:|
|==|Equals|
|!=|Not Equals|
|>|Greater Than|
|<|Less Than|
|>=|Greater Than Equals|
|<=|Less Than Equals|
|<=>|Combined comparision operator|

> the comparision operator used for sorting returns `0` if two values are equal,`1` if the first operand is greater and `-1` if the second operand is greater.


There are only two falsy values in Ruby `false` and `nil`.

Ruby has the following standard logical operators:

|Operators|Symbol|
|:-------:|:----:|
|&&|AND|
|`||`|OR|
|!|NOT|

Ruby also supports the idea of shortcut evaluation similar to the one used by Javascript.

Ruby has the following string methods:

|Methods|Description|
|:-----:|:---------:|
|upcase|uppercases the entire string|
|downcase|lowercases the entire string|
|capitalize|uppercases the first character|
|reverse|reverses a string|
|include?|checks if a substring is part of a string|
|split|splits a string to an array using a delimiter|
|gsub|replace every match of a regular expression with another string|
|to_sym|used to convert a string to a symbol|
|to_i|converts a string to an integer|
|intern|converts a string to a symbol|

> the method `to_s` can be used to convert a non string value to a `string`


Any method in Ruby that ends with a `?` returns a `boolean`.

---

`Arrays` in Ruby look like arrays in any other language:

```
an_array = [1,2,3,4,5]
```

Accessing elements by `index`:

```
an_array[2]
```

Pushing `data` to an array or a string can use the `<<` concatenation operator instead of the `push` method or the `+`.

```
alphabet = ["a", "b", "c"]
alphabet << "d" # Update me!

caption = "A giraffe surrounded by "
caption << "weezards!" # Me, too!
```

Arrays have the `each` iterator:

```
array = [1,2,3,4,5]

array.each do |x|
	x = x + 10
	print '#{x}'
end
```

Another way of using the `each` iterator:

```
array.each { 
    |x| 
    x = x * 2 
    print x
}
```

Another iterator is `times` which will execute an item a given number of times:

```
5.times { print "Dowtown Abbey" }
```

Iterating over multi dimensional array:

```
s.each {
    |x| x.each  {
       |y| puts y   
    }
}
```


If you know where iteration starts and how many times you would like to iterate over, you can use the `upto` and `downto` iterators instead of a `for` loop.

```
96.upto 100 do |x|
	puts x
end


"L".upto "P" do |x|
    puts x
end
```

`collect` is an iterator in Ruby that accepts a block and works like the `map` function in Javascript, if you need to mutate the original `array`, use `collect!`. In fact, `Ruby` does provide a `map` method which is an alias of the `collect` method described above.

`select` is an iterator that works like the `filter` function. There might even be an alias to `filter` for the method.


```
fibs = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55]

doubled_fibs = fibs.collect do |x|
    x * 2 
end
```

Sorting an array in the ascending order can be done using `sort!` without any arguments. Any method passed to `sort` must either return `-1`,`0` or `1` depending on whether the second item should come first, both items should have the same weight or the first item should come first.

```
books.sort! { |firstBook,secondBook|
	if firstBook < secondBook
		-1
	elsif firstBook > secondBook
		1
	else
		0
}
```

---

Ruby has a `hash` data structure(it is a data structure like the Python dictionary or the Javascript object):

> this is the `hash` literal notation

```
my_hash = {
	"name" => "Eric",
	"age" => 26,
	"hungry?" => true
}
```

There are two ways of creating an `empty` hash:

> if a key has no value, a default can be provided as an argument to `Hash.new`

```
empty_hash = Hash.new
empty_hash2 = {}

empty_hash_default = Hash.new("defaultValue")
```

Setting and getting values:

```
puts my_hash["name"] #get value from hash by key
my_hash["name"] = "Vamsi" #set value in hash  by key
```

To remove an entry from a `hash`, just use the `delete` method.

Accessing a value on a `hash` that does not exist causes a `nil` to be returned.

Iterating over a `hash` with `each`:

```
secret_identities = {
  "The Batman" => "Bruce Wayne",
  "Superman" => "Clark Kent",
  "Wonder Woman" => "Diana Prince",
  "Freakazoid" => "Dexter Douglas"
}
  
secret_identities.each do |superhero, alterEgo|
    puts "#{superhero}: #{alterEgo}"
end
```

`sort_by` is another iterator on `hash`:

```
frequencies = frequencies.sort_by { |word,count|
    count
}
```

In a `hash`, the `keys` are preferably `symbols`. They are written as:

```
{
	:x => 2
}
```

> Every object in Ruby does have an `is_a?` method that can be used to check if an item is an instance of the specified type.

A symbol is unique, all references to a symbol point to the same memory location.
Symbols are also used for referencing methods. Using symbols for defining hashes is
10,000 times faster than using strings.


There is a new style for defining hashes which is more concise:

```
{
	x: 2,
	y: 3,
	z: 4

}
```

> all keys are symbols in this notation.

A `hash` can be filtered for a set of keys that satisfy a condition:

```
my_hash.select {
	|key,value|
	value == 2
}
```

---

Methods:

To define a method:

```
def puts_1_to_10
	(1..10).each {|x| puts "#{x}"}
end

def cubertino(n)
	puts n ** 3
end

def add(a,b)
	return a + b
end
```

Creating and invoking a function without any paranthesis:

```
def alphabetize arr,rev=false
     arr.sort!
    if rev
        array.reverse!
    end
    arr
end

In `Ruby` the `return` statement can be made `implicit`, if no return statement is specified, Ruby will return the value of the `last statement`.

numbers = [1,4,5,2,3,5,2]

puts alphabetize numbers
```

> one can omit the `return` keyword, the last line of the method is automatically returned

`Splat arguments`: used when you have no clue how many arguments there are. an `argument` preceeded by a `*`.

```
def what_up(greeting,*bros)
	bros.each { |bro| puts "greeting #{bro}!"}
end
```

A method can have default parameters:

```
def alphabetize(arr,rev=false)

end
```
To invoke a method:

```
puts_1_to_10
cubertino(8)
```

If a method is not found, Ruby throws a `NameError`

> Paranthesis are usually optional in Ruby, its good practice to use paranthesis when calling a method.

`blocks` are anonymous methods. A named method can take an `anonymous block` as a parameter.

Ruby only cares about the methods that an object can respond to instead of the type of an object. So, Ruby provides a `respond_to?` method that accepts a `symbol` and determines if an object can respond to the message.

```
[1, 2, 3].respond_to?(:push)
"str".respond_to?(:to_sym)
4.respond_to?(:next)
```

If you do not want `ruby` to throw deprecation errors and so on, we need to add

```
$VERBOSE = nil
```

at the top of your code.

Blocks in `Ruby` **ARE NOT** lambdas. In a strange twist, every function that accepts a block is a generator that passes values to the block using the `yield` keyword.

```
def my_func(name)
	puts "Is going to yield"
	#block  takes control of the code
	yield
	puts "control returns to the function"
end

my_func("Jason")({ puts "The block has control"})

```

The output will look like:

```
Is going to yield
The block has control
control returned to the function
```

You can pass data to the `block` as arguments to `yield`:

```
def yield_name(name)
  puts "In the method! Let's yield."
  yield("Kim")
  puts "In between the yields!"
  yield(name)
  puts "Block complete! Back in the method."
end


yield_name("Vamsi") do |name|
	puts "My name is #{name}"
end
```

The output would look like:

```
In the method! Let's yield.
My name is Kim.
In between the yields
My name is Vamsi
Block complete! Back in the method.
```

Two things must be noted here:

+ you can yield multiple times to a block

+ you can pass data from a function to a block as arguments to the yield.

Blocks cannot be saved for reused as-is because they are not objects, if you need to save a block, you need to create a `Proc`. An example of a `Proc` looks like this:

```
round_down = Proc.new do |x|
    x.floor
end

floats.collect(&round_down)

```

The `&` operator converts a `proc` to a `block`. A `proc` has a method named `call` to invoke the `proc` without passing it to a method as a `block`.

```
hi = Proc.new {puts "Hello!"}
hi.call
```

`Symbols` in Ruby can be converted to `Proc` using the `&` operator.

```
numbers_array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

strings_array = numbers_array.map(&:to_s)
```

Lambdas are functions that can be used as callbacks:

> lambdas are defined using the `lambda` keyword. they can be invoked using `call` similar to a `proc`.

```
def lambda_demo(a_lambda)
  puts "I'm the method!"
  a_lambda.call
end

lambda_demo(lambda { puts "I'm the lambda!" })
```

It looks like lambdas can be stored in variables but cannot be named.

```
symbolize = lambda { |item| item.to_sym}
symbols = strings.collect(&symbolize)
```

Differences between `lambda` and a `proc`:

A proc will not validate the arguments passed to it. If fewer arguments are provided, it will just set the rest of the arguments to null. A lambda will throw an Error if any arguments are missing.

A proc will not return control back to the calling method unlike a lambda.

Ruby is an OO language, of course they have `class` syntax.

```
class Person
	def initialize(name)
		@name = name
	end
end
```

The `initialize` method acts as a constructor for a `class` in Ruby. Any `instance variables` are created using `@`. To create an instance of the class use

```
Person.new "Eric"
matz = Person.new "Yukihiro"
```

Static variables are defined using `@@` in Ruby. Global variables can either be defined simply outside a class or with `$` within a class.

To access a global variable defined with a `$`, you would still need to use a `$`.

```
class MyClass
  $my_variable = "Hello!"
end

puts $my_variable
```

You can use static variables like this:

```
class Person
  # Set your class variable to 0 on line 3
  @@people_count = 0
  
  def initialize(name)
    @name = name
    # Increment your class variable on line 8
    @@people_count += 1
  end
  
  def self.number_of_instances
    # Return your class variable on line 13
    @@people_count
  end
end

matz = Person.new("Yukihiro")
dhh = Person.new("David")

puts "Number of Person instances: #{Person.number_of_instances}"
```

Ofcourse, Ruby has `inheritance`, inherit a class using the `<` operator:

```
class Application
  def initialize(name)
    @name = name
  end
end

# Add your code below!
class MyApp < Application
end
```

To override a method, just define it again in your derived class. You still have access to the same method on the superclass using the `super` keyword.

```
class Message
    @@messages_sent = 0
    def initialize(from,to)
        @from = from
        @to = to
        @@messages_sent += 1
    end
end

class Email < Message
    def initialize(from,to)
        super
    end
end

my_message = Message.new("bruce@waynehq.com","diana@wwoman.org")
```

Ruby has access specifiers such as `public` and `private`. They are not added to individual methods but to sections of a class like:

```
class Dog
    #this makes all the methods from here to the end of the class public
    public
    def initialize(name,breed)
        @name = name
        @breed = breed
    end
    
    def bark
        puts "Woof!"
    end
   	#any method you defined from here will be private 
    private
    def id
        @id_number = 12345
    end
end
```

Ruby ensures that you would not have to setup accessors and mutators for your properties in your class. Instead, you can just:

```
class Person
  attr_reader :name
  attr_writer :name
  
  attr_reader :job
  attr_writer :job
  
  def initialize(name, job)
    @name = name
    @job = job
  end
end
```

which is equivalent to writing:

```
class Person
  def initialize(name, job)
    @name = name
    @job = job
  end

  def name
  	@name
  end

  def name=(name)
  	@name = name
  end

  def job
  	@job
  end

  def job=(job)
  	@job = job
  end
end
```

To make a variable both readable and writable using just a single line using `attr_accessor`:

```
class Person
  attr_reader :name
  attr_accessor :job
  
  def initialize(name, job)
    @name = name
    @job = job
  end
end

person = Person.new("vamsi","idiot")
puts person.job
```

Modules in `ruby` are similar to classes but can only contain class methods, they cannot be instantiated and they cannot have subclasses. A module can store constants but cannot contain variables.

Create a module with a simple constant:

```
module MyLibrary
	FAVE_BOOK = "The girl with the dragon tattoo"
end
```

To lookup something from a module, use the `::` operator, this is known as the `scope resolution operator`

```
Math::PI
```

If a module has not already been loaded, it would have to be loaded using a require statement:

```
require 'date'
```

A class can use any constants or methods within a `module` using the `include` statement:

```
class Angle
	include Math
end
```

This will allow the class to use any members of the class without having to use the `::` operator i.e the module can act as a `mixin`.

Using a module as a mixin:

```
module MartialArts
    def swordsman
        puts "I'm a swordsman."
    end
end

class Ninja
  include MartialArts
  def initialize(clan)
    @clan = clan
  end
end

class Samurai
  include MartialArts
  def initialize(shogun)
    @shogun = shogun
  end
```

Mixins can also be possible at the class level using `extend`:

```
module ThePresent
  def now
    puts "It's #{Time.new.hour > 12 ? Time.new.hour - 12 : Time.new.hour}:#{Time.new.min} #{Time.new.hour > 12 ? 'PM' : 'AM'} (GMT)."
  end
end

class TheHereAnd
  extend ThePresent
end

TheHereAnd.now
```