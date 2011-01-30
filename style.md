# Coding Style

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
