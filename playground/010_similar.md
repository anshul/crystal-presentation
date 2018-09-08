# Similarities

## Crystal is very similar to ruby

### Similar syntax, blocks, enumerables and stdlib
```playground
p (1..5).to_a
  .sort { |a,b| b<=>a}
  .reject { |a| a.even? }
```

### Similar oop, class, implicit return
```playground
class Adder
  def initialize(a : Int32)
    @a = a
  end

  def add(b)
    @a + b
  end
end
a = Adder.new(5)
a.add(2)
```

### You can re-open classes

```playground
class Aa; def b; 1 end end
class Aa; def b; 2 end end
Aa.new.b
```


### We have modules and mixins just like you would expect
```playground
module Cc; def c; 'c' end end
class Aa; extend Cc end
class Bb; extend Cc end
Aa.c == Bb.c
```

### Feels like idiomatic ruby!
```playground
def do_something
  puts "hey everyone"
end

def you_shouldnt?
  false
end

do_something unless you_shouldnt?
```

```playground
class Foo
  @memo : Int32?
  def a(i)
    @memo ||= i * i
  end
end
foo = Foo.new
foo.a(5)
foo.a 2
```

### Spec is built in
```playground
require "spec"
describe "thing" do
  it "works" do
    (1+2).should eq(3)
  end
end
```

### Code feels very rubyish so it's easy to get up to speed quickly

