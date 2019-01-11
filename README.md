# MiniService
MiniServices are a prototype from which to build single-functionality
 minimalistic services, aiming to
help you correctly modularize and isolate your processes making them easier to
mantain and less prone to
errors.

## Usage
You can use `rails generate mini_service YourServiceName` to create a template
file inside your app/services
directory with the provided name.

Otherwise you can create or modify your own services by inheriting
from `MiniService::Mini` class.

Your `MiniServices` should be used via their `call` method, providing arguments
in a hash, like
`ExampleService.call(p1: v1, p2: v2)` or `ExampleService.call(args)` with args
built elsewhere.

This will automatically initialize your service with one `@instance_variable`
for each `key-value` pair
you've given.

So for example a service like this:
```ruby
class ExampleService < MiniService::Mini
  private

  def perform
    # TODO: put your service logic in here~!!
  end
end
```

when called like this: `ExampleService.call(ex: true, ample: 1)`, would have
both `@ex = true` and
`@ample = 1` set.

The `perform` method you see in the example, is the only method that will be
run when you `call` a
`MiniService`; that is, all your logic should be put there, and the final
result should be `return`ed as the
service's response.

Also, `MiniServices` provide a nice way of declaring which arguments should be
required and let through, raising errors when this conditions are not met.
You can declare them using `mini_reqs` and `mini_lets` methods on your class'
definition, giving them each an array of symbols.

```ruby
class ExampleService < MiniService::Mini
  mini_requires %i[a1 a2]
  mini_allows %i[a3 a4]

  private

  ···

end
```

So it would raise `MissingArguments` or `UnallowedArguments` if you miss `a1`
or add `a5` respectively

## Installation
Add this line to your application's Gemfile:

```ruby
gem 'mini-service'
```

And then execute:
```bash
$ bundle
```

Or install it yourself as:
```bash
$ gem install mini-service
```

## Contributing
If you wan't to contribute you can contact me via github or directly fork the
repository and then make a
pull request.
For now, I'll only accept improvements on the code or functionality directly
mentioned in the Next Changes
section.

## Next Changes

Testing the whole service, maybe provide a more complete generator, provide
further options for variables declarations.

## License
The gem is available as open source under the terms of the [MIT License](https://opensource.org/licenses/MIT).
