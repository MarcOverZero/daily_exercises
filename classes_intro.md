PREFACE: Classes are storage containers. They contain, usually, two things: VARIABLES,
and METHODS.

A class has no purpose without methods. Even if you put a bunch of 
instance variables inside of a class like so: 

```
class Dog
  @name = "fido"
  @age = 5
  @color = "tan"
end
```

In the above, you would never be able to call/retrieve any of those instance variables, or 
change them. Therefore, a class COULD have methods only, and function, but a class 
COULD NOT do anything useful with variables only. Also, classes in Ruby are made to use 
both methods and variables together so you can store values(variables), and retrieve or change 
values(methods).

IN YOUR CONSOLE

1. Make a class `Dog` as illustrated above. Then do: `Dog.new`. Note that the object returned has no 
instance variables indicated in it. Example: What you got(or similar): `#<Dog:0x007fb8819cb9e0>`.
What you may have expected: `#<Dog:0x007fb881359b48 @age=5, @name="fido">`. Instance variables are not 
stored in local memory until a method declares them. That's why initialize is so handy for assigning values 
to your instance variables, because when you do `Dog.new`, initialize is automatically invoked if it's in your 
class (NOTE: You don't have to have an initialize method to make a class work, but if you do, the `.new` method, 
which is a built-in method in Ruby, will call initialize, setting up your instance variables in local memory).

2. Make a class `Kitty`:

```
class Kitty
  def initialize
    @name = "Fuzzy"
    @age = 7
  end
end
```

Now when you do: `kitty = Kitty.new`, you will see that your kitty variable holds an 
object that has instance variables indicated in it. Something like this: `#<Kitty:0x007ff00c035a30 @age=7, @name="Fuzzy">`. 
That's cool, but we still can't use those instance variables. They exist, but they serve no 
purpose because our class doesn't have any methods to use them. For fun, try to get the 
kitty's name. If you succeed, how many hoops did you have to jump through?

3. Make a class `Person`:

```
class Person
  def initialize
    @name = "Bob"
    @age = 22
  end
  
  def name
    @name
  end
  
  def age
    @age
  end
```

Instantiate your `Person` class, assigning it's value to the local variable `bob`:
`bob = Person.new`. Now you can call methods on that object/value: 
`bob.name` #=> `"Bob"`, `bob.age` #=> 22. <br>
This would be great if we only ever needed our person to be named "Bob", and age 22, but if we 
want to create/instantiate multiple `Person` class objects with different names and ages, we will 
need to either have a method(s) that changes the name and age (impractical), or we will want to 
pass those values in when instantiating. When you do: `Person.new`, the `.new` method has the 
ability to pass values to the `initialize` method in the class, if there is one. 

4. Remake your class, typing it just as shown, even if it looks weird:

```
class Person
  attr_reader(:name, :age)
  
  def initialize person_name, person_age
    @name = person_name
    @age = person_age
  end  
```

If you've done mythical creatures or used the attr methods before, you may notice it looks different 
up there than it usually does, because there are parens. The convention is to NOT use parens with the 
attr methods, but my point in using them is to show you that it IS just a method, and the symbols 
in the parens are just arguments you are passing to it. Parens are optional when using arguments with 
methods, as shown in the initialize method, which now doesn't have any parens. Ruby doesn't care, it 
only needs each argument separated by a comma, and either a space or enclosing `()` after the method 
name. TIP: Use parens when you can, as that adds clarity and makes your code more understandable at a 
glance.

The `attr_reader` is just a dumb method maker. When you use it, what it does is make you an "invisible" 
method that only pops up when you instantiate a new instance of your class (what it actually does is 
append that method to the method table created in local memory during instantiation, but thinking of 
it as an invisible method in the class may help conceptualize at first). The way it makes the method is 
it just takes off the `:`, says `def whatever_symbol_you_gave_it`, one the next line adds an `@` to the 
symbol you gave it, then on the next line it uses `end`. This is paraphrasing the way it builds the 
method, but that's essentially it. So when you do: `attr_reader :name`, Ruby does:

```
def name
  @name
end
```

That's it. There is nothing else the attr_reader can do. It can't take special code, or add anything 
besides `@name` inside of it, so this attr is only good for making a convenience method(or methods)
that return(s) an instance variable named the same thing as the symbol(s) you give as arguments.
This may make you think "why even do that when you can just make those methods yourself". What happens 
when you have 100 instance variables and 50 of them need to be returned using `.the_thing`. Now 
your file has, counting spaces, ~200 extra lines of code to go through when reading it. In 10 lines 
or less you can use attr_reader with 50 arguments that will save you space and make your code easier 
to traverse.

5. Goto or make a practice directory (It doesn't have to be named practice). You will be making several
   files in it.

6. In your practice directory, make a file called dog.rb, using `touch` from the console. Don't use your 
   editor to make it.
   
7. Open the dog.rb file in your IDE/editor, and make a method in it that returns the dog's name. No 
   class yet, just the method. Just below the name method, call it and use puts to display it's return 
   value in the console (using a method name while it is IN scope, in this case it's in the file
   where the method is defined, and the method isn't wrapped in a class, so it's in scope anywhere
   in the file after the method is defined.)
   
```
def name
  "Fido"
end

puts name
```

Run the file. You can see that Ruby will run in a file just fine, without a class. When it does this, it 
will run top to bottom, meaning it can't retrieve any values that are stored in methods/variables, and 
it can't run any methods, unless they are defined/assigned ABOVE where they are use. The 
same is true inside a method, but this is NOT true inside of methods in a class, where the entire 
object is set up for us when we instantiate it, and we can call methods above where they are 
defined and Ruby will be able to understand. We will look at that later.

8. In your dog.rb file, move the `puts name` line above the method, just to see that Ruby won't be able 
   to do that. You can also define variables in a file just fine, but if you try to use 
   a variable that's not defined inside a method, it needs to be an instance variable (or a CONSTANT works
   too). Move your `puts name` back down, and above the method, assign the string "Fido" to a 
   local variable `dog_name`. Then use `puts` to output it to the terminal/console. Your file should look
   like this:
   
```
dog_name = "Fido"

def name
  "Fido"
end

puts name
puts dog_name
```

And you should get two Fido's when you run the file.

9. Replace `"Fido"` inside of the name method with your dog_name local variable and run the 
   file. Does Ruby understand what dog_name is inside the method? It shouldn't, because 
   dog_name is a local variable, and local variables can't be seen if they aren't inside the 
   "wrapper" that's trying to use them. In this case the "wrapper" is our name method, and the 
   local variable would need to be defined inside the method in order for it to work. Change 
   the name method so that dog_name is assigned/defined inside of it, like so:
   
```
def name
  dog_name = "Fido"
  dog_name
end

puts name
puts dog_name
```

Now what happens when it tries to use the `puts` method on dog_name? It's in the method "wrapper", so 
the file "wrapper" can't see it anymore. Local variables are great for creating and transitioning 
values temporarily. <br> 
NOTE: Part of Ruby's implicit return (that's when Ruby gives you the last thing evaluated in a method 
when it's called/invoked) is to return values that are assigned as the last thing in the method. This 
means you can take out the `dog_name` line below `dog_name = "Fido"`, and the `puts name` line will 
still work just fine. Remove the `dog_name` line and the `puts dog_name` line, and run the file.

10. Instance variables CAN be seen inside of methods, even if they aren't created inside of them. Let's 
    see that in action. At the top of your file, assign the value `"Fido"` to the instance variable `@dog_name`.
    Get rid of the local variable assignment inside of your `name` method. The local variable assignemt is 
    the line that looks like this: `dog_name = "Fido"`. It's called a local variable assignment because it 
    uses the assignment operator, `=`, to assign/attach a value to a local variable. In place of that 
    `dog_name = "Fido"` line, we will put the line `@dog_name`. That's it. Your file should look like this:

```
@dog_name = "Fido"

def name
  @dog_name
end

puts name
```

This should give you `Fido`

11. Instance variables can be seen from inside a method, and they can also be seen from outside a method. More 
    correctly, instance variables can be seen be both the inner(the method in this case) and outer(the file)
    wrappers. To see this, put the `@dog_name = "Fido"` line inside the `name` method, at the top. Just under 
    the `puts name` line, add `puts @dog_name`. `@dog_name` is declared/defined/assigned inside the `name` method, 
    but thanks to the awesomeness of instance variables, Ruby will still have access to it at the file level. 
    Your code should look like this, and you should run the file:
    
```
def name
  @dog_name = "Fido"
  @dog_name
end

puts name
puts @dog_name
```  

And to reiterate, implicit return will handle the return of the value that's assigned to `@dog_name` without us 
needing the line `@dog_name` inside the method. Remove that line, run the file, and see that it works.

The neat thing about instance variables is that, when you instantiate a class, they are stored temporarily for
you in your computer's local memory, and they stay in local memory until your class is finished running it's
code/methods. This has to do with the stack and the HEAP, and technically the instance variables are stored in 
the HEAP, but just remember that instance variables can be used to create, change, and retrieve values any time 
during any method's execution, whereas local variables "pop" off of the stack after a method finishes running. 

Why does this matter? Because now you can keep track of "state" while your class is doing stuff. If you needed a 
counter to keep track of the number of times a certain method runs, you couldn't just make it a local variable, 
because every time that method runs, the local variable is once again assigned, erasing any increments your 
counter has performed. Example:
    
```
def add_to_count
  counter = 0
  counter += 1
end
```

Each time this method runs, it's reset to 0, then it's set to 1, and it will never actually increase over 1. BUT, 
with an instance variable, you can change the value in one method, and another method could retrieve that value, 
seeing it change as methods are run again and again. Example (you would want an initialize here for your instance 
variable so I'm including it):

```
def initialize
  @counter = 0
end

def add_to_count
  @counter += 1
end

def check_counter
  @counter
end
```

12. Add an instance variable `@name` to your file at the top, and set it equal to `"Fido"`, then change your `name` 
    method to return `@name`. Add a method `change_name` to your file that lets you change the dog's name. Finally, 
    change the name at the bottom of the file to see that it works.

```
@name = "Fido"

def name
  @name
end

def change_name(new_name)
  @name = new_name
end

puts name
change_name("Lady")
puts name
```  

This shows us that instance variables don't need to live inside of classes to work. BUT, the way Ruby is designed, 
instance variables work best when combined with an initialize method inside of a class. That way you can carry the 
instance variables around with you more easily and organize your code better.

We've seen that Ruby can make variables and methods, and run those methods and any other code in a top-down manner 
if we just put stuff in a file. This is fine if you are only dealing with a few methods and variables, but what 
happens when you have 50, or 100 methods, and as many variables flying around? That's why, for your own sanity, you 
should use Ruby's file/class/methods/variables container system to organize your code. For the most part, the system
works in that order. Files contain classes, classes contain methods, methods contain variables. There are things like 
constants that may float around outside of methods, and you may have code at the bottom of a file, outside a class, that 
runs that class's methods. Also, these containers are like legos, in that a seemingly bigger piece can snap on to a 
seemingly smaller piece. Meaning, if you wanted to, you could create an array that has 1000 class objects in it, then 
assign that array to a local variable. Now you have a local variable that holds and array, that holds classes, that 
each holds methods and variables... It can start to make you cross-eyed, but just remember that any Ruby object can 
hold any other Ruby object, or objects if you are using a collection (arrays, hashes, etc.). 

FOR NOW: Concentrate on files holding classes, which hold methods and variables. Data Structures, otherwise known as 
collections (hashes, arrays, etc.) are values that hold other values. So think of them as sub-containers you can use
inside of your class when you want to have more than one value assigned to a variable (or returned by a method). 

RECAP:<br>
a. Files hold anything that's Ruby legal (variables, classes, methods, code execution, etc.)

b. Classes hold methods in a convenient wrapper/container.

c. Methods hold executable code, variables, and can be used to return a value just like a variable would.

d. Variables hold values. A value is ANY legal Ruby object.

e. Examples of legal Ruby objects: 
- Data Types: integers(5), strings("hello"), booleans(true/false), symbols(:hello), nil
- Data Structures: hashes(`{:hello => "hello"}`), arrays(`[1, 2, 3]`), structs, linked lists, binary trees, tries, etc.
- Class instantiations: `dog = Dog.new`
  

