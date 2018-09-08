# Some differences I really like!

### This @initialize needs to be ported back to ruby

```playground
class Greeter
  property name : String

  def initialize(name, salutation = "Hello")
    @name = name
    @salutation = salutation
  end

  def greet
    "#{@salutation}, #{@name}"
  end
end

g = Greeter.new("Will")
g.greet
g.name
g.name = "Alice"
g.greet
```

```
➤ crystal tool hierarchy -e Greeter g.cr
- class Object (4 bytes)
  |
  +- class Reference (4 bytes)
     |
     +- class Greeter (24 bytes)
            @name       : String (8 bytes)
            @salutation : String (8 bytes)
```

### `&.` is so much better than `&:`
```playground
a = %w[apple bat cat]

a.map(&.upcase)

a.map(&.reverse.upcase)

a.map( &.split(//).sort.join )
```

