# Coding Style

## Operators

### Making sense with Ruby's "unless" 

Some rules of thumb when using unless:

* Avoid using more than a single logical condition. `unless foo?` is fine. `unless foo? && bar?` is harder to parse.
* Avoid negation. "Unless" is already negative. Piling more on only makes it worse.
* Never, ever, ever use an `else` clause with an `unless` statement.

###### Good Examples

```ruby
i += 1 unless i > 10

unless person.present?
  puts "There's no such person" 
end
```

###### Bad Examples

```ruby
unless !person.present? && !company.present?
  puts "do you even know what you're doing?" 
else
  puts "and now we're really confused" 
end
```

Inspired by [37signals][1].


## Blocks

### { ... } blocks versus do ... end blocks

There are two prevailing conventions on when to use curly braces for blocks versus the do ... end keywords:

* You MUST use curly braces for one-line blocks, use do ... end for multi-line blocks
* You MUST use curly braces when the return value is desired (or chained), use `do ... end when the side-effect is desired

The latter convention seems to be gaining in popularity, but there does not seem to be consensus on this issue at the time of this writing.

Note: The two block notations have different precedence, so they are not always interchangeable unless parentheses are used.

```ruby
class Post < ActiveRecord::Base

  # The following statement raises a compile error
  scope :search_for, lambda { |query|
    where("1 == 1")
  }

  # The following statement works
  scope :search_for, lambda { |query|
    where("1 == 1")
  }

end
```

## Methods

### Don't put spaces between a method name and its parameter list

Make the precedence rules clearer: never leave a space between the end of the method invocation and an open parenthesis. Butt the parameter list up tight against the name of the method.

    # parses visually the same way Ruby parses it
    Math.sqrt(2 + 2) * 3 

but

    # is confusing
    Math.sqrt (2 + 2) * 3

The same applies to method definition

    # good version
    def say(message = "hello)
    end

    # bad version
    def say (message = "hello)
    end

    # bad version
    def say( message = "hello )
    end

_Suggested by Dave Thomas on RubyGardens.org._


### Put parentheses around non-trivial parameter lists

If you have a method parameter that involves any degree of complexity or that starts with a parenthesized expression, put the whole parameter list in parentheses.

This can be a cause of some pretty subtle bugs, so it's worth getting into the habit of using parenthesized parameter lists. Apart from a few common idioms such as

* `require "name"`
* `attr :name`

where parentheses would seem strange, it's rarely a mistake to add them.

Precendence rules sometimes make it difficult to understand why a method call gives the answer it does. For example, the following came up in RubyTalk:12899.

    p(2.4/0.2).to_i    # -> 12.0
    p((2.4/0.2).to_i)  # -> 11

A poster wanted to know why (x) != x.

Of course what's really happening is that Ruby is treating the parenthesis after the `p` as the start of a parameter list. The matching closing parenthesis then closes the parameter list, and anything that follows it gets applied to the result of the function.

_Suggested by Dave Thomas on RubyGardens.org._


  [1]: http://37signals.com/svn/posts/2699-making-sense-with-rubys-unless
