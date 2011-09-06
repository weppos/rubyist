## Extensions

##### WARNING:

Thought Ruby allows you to reopen classes, you shouldn't abuse that feature. In particular, avoid changin existing methods, especially in the Ruby core or standard library. If you change the behavior of a method, your application might now working properly.

If you decide to add a new method, make sure you are using an unique name. Otherwise, if you are using a Gem which defines a method with the same name, something might not work as expected.

Be careful when you modify existing classes. Consider using [Inheritance][1] or [Composition][2].


### Ruby, Rails & Gem extensions

Sometimes you need to <strike>monkeypatch</strike> extend a specific Rails library, a Ruby core class, or a Gem. The flexibility of Ruby allows you to reopen an existing class/module to add new methods or modify existing ones.

The most common question is: where should I write these extensions? In fact, there are several places where these files can be stored, however not all folders are loaded at the same time. Also, some folders are not loaded at all (unless you require them) making your <strike>hack</strike> customization even less elegant.

The following convention solves the problem attempting to respect the purpose of each Rails folder.

Create an initializer with the following content and save it in the `/config/initializers/` folder. The file name MUST be `_extruby.rb` The name SHOULD be prefixed with a `_`, in this way Rails will load this file before all the other initializers in the same folder.

    Dir[File.expand_path("../../../lib/extruby/**/*.rb", __FILE__)].each { |f| require f }

Create the folder `/lib/extruby` which will contain all the extensions. The name of the folder MUST match the name of the initializer, without the `_`. To better organize the files, you SHOULD organize the extensions according to the following folder structure:

 # TODO: explain structure

    lib/extruby/
    ├── active_record
    │   └── sqllike.rb
    ├── mail
    │   ├── address.rb
    │   └── clone.rb
    ├── money
    │   └── money-rails.rb
    ├── postageapp
    │   └── actionmailer.rb
    ├── public_suffix_service
    │   └── domain.rb
    ├── ruby
    │   └── core
    │       ├── object_delayed_job.rb
    │       └── object_yielding.rb
    └── whois
        ├── elabtime.rb
        └── super_struct.rb

Remember that Ruby extensions MUST be tested as any other method. Depending on your test framework (`Test::Unit`, `Shoulda`) you SHOULD create a corresponding test suite for any customization.

 # TODO: update structure

    spec/lib/extruby/
    ├── mail
    │   └── address_spec.rb
    ├── money
    │   └── rails_spec.rb
    ├── ruby
    │   └── core
    │       └── object_yielding_spec.rb
    └── whois
        └── super_struct_spec.rb


##### Considerations

The solution presented above attempts to respect the purpose of each Rails folder.

1. It uses an initializer, so that the extensions are loaded when the Rails framework is loaded. However, the extensions are not stored in the initializers folder to avoid cluttering the namespace.
1. It prefixes the initializer with _ causing the initializer to be loaded before any initializer, making the extensions available as soon as possible.
1. It uses a dedicated folder in the `lib` folder to store all the _library_ extensions.

  [1]: http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)
  [2]: http://en.wikipedia.org/wiki/Object_composition
