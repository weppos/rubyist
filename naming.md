# Naming Conventions

## Constants

Constants MUST use `UPPER_CASE`.

```ruby
Math::PI
OptionParser::REQUIRED_ARGUMENT

class Curses
  KEY_DOWN = nil
end
```

## Classes and Modules

Classes MUST use `PascalCase`. Join words of class names by capitalizing the first letter of each word. The same goes for `ModuleNames` as well.

```ruby
class MyClass
end

module MyModule
end
```

## Methods and Variables

Methods MUST use `underscore`, as do `local_variables`, `@instance_variables`, and `@@class_variables`. Join words with underscores (aka `snake_case`).

```ruby
class Greeter
  @@hello = nil
  @@hello_message = nil

  def hello
    @hello = nil
  end

  def say_hello
    @say_hello = nil
  end
end
```

Keep acronyms in class names capitalized. `MyXMLClass`, not `MyXmlClass`. Variables should use all lower-case.

## Important

There is no place in Ruby where `camelCase` is ever used.
