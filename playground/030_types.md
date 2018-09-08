# Let's talk about static dispatch

### This is actually 2 methods!
```playground
def double(i)
  i * 2
end

answer = double(3)
puts typeof(answer)

answer2 = double("hi")
puts typeof(answer2)
```

### Inferred union types
```playground
def validate(i)
  if i > 10
    i
  else
    "too low"
  end
end

hi = validate(15)
hi.class
typeof(hi)

lo = validate(1)
lo.class
typeof(lo)

# hi * 2 # if hi
# lo * 2 # if lo

# lo + 2
# hi + 2

# ok let's get rid of the else

# (hi as Int32) + 2
# hi.not_nil! + 2
# (lo as Int32) + 2
```

### Overloading looks like this...
```ruby
def foo(a,b)
  if b.kind_of? String
    case a
    when Fixnum
      1            # foo(3, "c")    # => 1
    when TrueClass
      2            # foo(true, "c") # => 2
    else
      3            # foo(:hi, "c")  # => 3
    end
  else
    4              # foo(:hi, :c)   # => 4
  end
end
```


```playground
def foo(a : Int, b : Char)
  1
end

def foo(a : Bool, b : Char)
  2
end

def foo(a, b : Char)
  3
end

def foo(a, b)
  4
end

foo 3, 'c'
foo true, 'c'
foo :hi, 'c'
foo :hi, :c
```

### Abstract classes for interfaces
```playground
class Animal end

class Dog < Animal
  def talk; "Woof" end
end

class Cat < Animal
  def talk; "Meow" end
end

class Person
  getter pet : Animal

  def initialize(@name : String, @pet) end
end

will = Person.new "Will", Dog.new
alice = Person.new "Alice", Cat.new

p will.pet.talk
```

### Some container types

```playground
a = [ [1,'a'], [2,'b'] ]
# a << ['c', 3]
# a.first.first + 100

b = [ {1,'a'}, {2,'b'} ]
# b << {'c', 3}
b.first.first + 100

# c = []
```

# Literal types


```
Nil	nil
Bool	true, false
Integers	18, -12, 19_i64, 14_u32,64_u8
Floats	1.0, 1.0_f32, 1e10, -0.5
Char	'a', '\n', 'あ'
String	"foo\tbar", %("あ"), %q(foo #{foo})
Symbol	:symbol, :"foo bar"
Array	[1, 2, 3], [1, 2, 3] of Int32, %w(one two three)
Array-like	Set{1, 2, 3}
Hash	{"foo" => 2}, {} of String => Int32
Hash-like	MyType{"foo" => "bar"}
Range	1..9, 1...10, 0..var
Regex	/(foo)?bar/, /foo #{foo}/imx, %r(foo/)
Tuple	{1, "hello", 'x'}
NamedTuple	{name: "Crystal", year: 2011}, {"this is a key": 1}
Proc	->(x : Int32, y : Int32) { x + y }
```

