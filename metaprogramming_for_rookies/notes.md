Metaprogramming — code that writes code

__The purpose of this talk is to:__

1. Teach you that metaprogramming is happening behind the scenes in many places you are already familiar with.
2. Give you the tools you need to define powerful dynamic methods on the fly.
3. Most importantly: Boost your understanding of Ruby fundamentals by exploring the nuances of the language and not being afraid to dig around.

Rewrite attr_reader method to show how metaprogramming work

Creating Dynamic Methods with `class_eval`

```
ClassName.class_eval { def method_name; @instance_var; end }
```

```
new_method = %Q{
   def find_by#{some_value}_and_#{other_value}
      # method does something
   end
}

ClassName.class_eval(new_method)
```

class_eval vs. instance_eval

So if you only want to define a method for a single instance, you can use the instance_eval method. If you instead want to dynamically define methods that are accessible to every instance of a class, you would call the class_eval method on a class object

## Talk

"to become a Ruby Jedi, you have to master the art of metaprogramming" – I made that up

What is metaprogramming? Is it magic? It is not, though it is certenly magical.

This talk is separated into two section:

1. Section 1: A brief intro about metaprograming and discussing few techniques
2. Section 2: A quick tutorial about how to build something magical (yet useless) using metaprograming

Spells:

- Open Classes (aka Monkeypatch)

```
class String
  def upcase?
    self == self.upcase
  end
end
```

The Dark Side: if you casually add bits and pieces of functionality to classes, you can accidentally overwrite the a method that some other parts of the code base relying on.

- Dynamic Method

- Ghost Method

- Dynamic Dispatch

Why would you use send instead of the plain old dot notation? Because with send, the name of the method that you want to call becomes just a regular argument. You can wait literally until the very last moment to decide which method to call, while the code is running.

## Section 2

Assupmtions

- Each JSON containes data for a single element
- JSON object doesn't have any nested attributes
- JSON key names doesn't contain and special characters or spaces
