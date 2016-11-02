+ strings written with `''` do not perform string interpolation, they do not escape certain sequences such as `\n`

+ strings written with `""` allow string interpolation

+ strings can be multiline, they have to use the `"""` at the beginning and the end of the string:

```ruby
"""
This is a multiline
string in Ruby written
with three double quotes
as a delimiting token
"""
```

+ strings can have escape sequences embedded within them:

```
"this ain\'t my fault \\ i didn't lead a revolt\nyou wouldn\'t gives us our salt\t and that\'s it"
```

+ strings can also be writen using a `heredoc` style:

```ruby
poem = <<END
there is no poetry
but i have heard of nerd tree
and vinegar, i know, i know
that none of this is sensible
END
```

> you write `<<` followed by an uppercase delimiter like END, the string begins on the next line and ends when the delimiter is encountered again. here, the string is between the `END` tags.

+ when you would like to pass command-line arguments to a ruby program and use them in your program, you can read them off of `ARGV`

```ruby
first, second = ARGV
f = ARGV.first
```

> If there is only one argument expected, the destructuring style wont work, in such cases you should use the `first` method on `ARGV`.

+ `ARGV` messes with `gets.chomp`, instead of `gets.chomp`, use `$stdin.gets.chomp`.

+ The `puts` command can also be used with a custom formatter:

```ruby
formatter = "First, I did %{first}, followed by %{second}, then she said %{third} and I %{fourth}"
puts formatter % {
  first: "brain surgery",
  second: "occult rituals",
  third: "are you crazy?",
  fourth: "ran away"
}
```

+ `puts` also accepts `C style formatters` as well:

```ruby
formatter = The number of %s is %d
puts formatter %, "apples",24
```

+ The `File` API in Ruby looks like:

|Method|Description|
|:----:|:---------:|
|File.exists?|determines if a file exists when provided with a path to a file|
|File.open|opens a file in the provided mode and returns a `File` instance, can also be used as `open`|
|File#seek|places the read pointer at the given line within the file from a given offset|
|File#read|reads a file using the mode provided or defaults to `r`, returning the `length` in bytes| 
|File#truncate|deletes the contents of a file, leaving it empty|
|File#write|writes to a file|
|File#close|close a file once we are done with it|

> The modes for open and read are as follows: `r` for read, `w` for write and `a` for append. if a file needs to be opened in both read and write mode use `r+`, `w+` or `a+`.

+ to require a module use `require 'relative_path/to/file/name'`

> you can use this from `irb`, the module will automatically be available in the current scope without having to explicitly set it to a value.

> Ruby's `<>` was also used to mean `!=` but the former operator was deprecated and the latter is much preferred.

---
