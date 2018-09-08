# Macros for metaprogramming

```ruby
class Object
  macro getter(*names)
    {% for name in names %}
      {% name = name.var if name.is_a?(DeclareVar) %}

      def {{name.id}}
        @{{name.id}}
      end
    {% end %}
  end
end

class Person
  getter name, age
end

class Person
  def name; @name end
  def age; @age end
end
```

### shell out

```ruby
macro buildtime
  "{{`date`}}"
end

puts buildtime
puts `date`
```

```ruby
➤ crystal build bt.cr && ./bt
Wed Dec  9 12:09:51 JST 2015
Wed Dec  9 12:09:51 JST 2015
➤ ./bt
Wed Dec  9 12:09:51 JST 2015
Wed Dec  9 12:10:28 JST 2015
➤ ./bt
Wed Dec  9 12:09:51 JST 2015
Wed Dec  9 12:11:01 JST 2015
```

