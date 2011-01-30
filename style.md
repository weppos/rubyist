# Coding Style

Coding style and development conventions.

## Naming Conventions

The following conventions are constraints set by the Ruby language.

### Constants

Constants MUST use `UPPER_CASE`.

##### Examples

```ruby
Math::PI
OptionParser::REQUIRED_ARGUMENT

class Curses
  KEY_DOWN = nil
end
```

### Classes & Modules

Classes MUST use `PascalCase`. Join words of class names by capitalizing the first letter of each word. The same goes for `ModuleNames` as well.

##### Examples

```ruby
class MyClass
end

module MyModule
end
```

### Methods & Variables

Methods MUST use `underscore`, as do `local_variables`, `@instance_variables`, and `@@class_variables`. Join words with underscores (aka `snake_case`).

##### Examples

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

### Acronyms

Keep acronyms in class names capitalized. `MyXMLClass`, not `MyXmlClass`. Variables should use all lower-case.

### camelCase

There is no place in Ruby where `camelCase` is ever used.

## Operators

### Making sense with Ruby's "unless" 

Some rules of thumb when using unless:

* Avoid using more than a single logical condition. `unless foo?` is fine. `unless foo? && bar?` is harder to parse.
* Avoid negation. "Unless" is already negative. Piling more on only makes it worse.
* Never, ever, ever use an `else` clause with an `unless` statement.

##### Good Examples

```ruby
i += 1 unless i > 10

unless person.present?
  puts "There's no such person" 
end
```

##### Bad Examples

```ruby
unless !person.present? && !company.present?
  puts "do you even know what you're doing?" 
else
  puts "and now we're really confused" 
end
```

Inspired by [37signals][1].


  [1]: http://37signals.com/svn/posts/2699-making-sense-with-rubys-unless
