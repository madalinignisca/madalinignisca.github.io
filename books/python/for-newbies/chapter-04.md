---
layout: page
title:  "Chapter 4: Functions – The Building Blocks of Reusable Code"
last_modified_at: 2024-02-12 12:12
---
- [Defining Functions]({{ site.baseurl }}#defining)
- [Function Parameters and Return Values]({{ site.baseurl }}#params)
- [Variable Scope]({{ site.baseurl }}#scope)
- [Docstrings]({{ site.baseurl }}#docstrings)

## Defining Functions {#defining}

In this subchapter, we'll explore one of the most powerful tools in Python and indeed all of programming: functions. A function is a reusable block of code that performs a specific task. Once defined, it can be executed or "called" any number of times throughout your program.

### What Are Functions?

Think of functions like little helpers that take care of tasks for you. In real life, if you have a complex task to do repeatedly, such as preparing your favorite recipe, you might write down the steps so you don't have to remember them each time. Similarly, in programming, when you find yourself needing to perform the same action multiple times within an application, writing a function for that action is beneficial.

Functions help make our code:
- **Reusable**: We can write the logic once and use it many times.
- **Organized**: Functions allow us to structure our code into manageable chunks.
- **Maintainable**: If we need to change how a particular piece of functionality works, we only need to update it in one place.

### How To Define A Function

To define a function in Python, we use the `def` keyword followed by the name of the function and parentheses `()`. Inside these parentheses are parameters (also known as arguments) through which we pass values into our function. The body of the function follows after a colon `:` and is indented:

```python
def greet():
    print("Hello there!")
```

This simple example defines a function named `greet` that takes no parameters and prints out "Hello there!" when called.

### Calling A Function

Once defined, calling or invoking this function is done by using its name followed by parentheses:

```python
greet()
```

When run, this will output:

```
Hello there!
```

### Parameters And Arguments

Most functions will take some kind of input they work with called parameters (or formal parameters). When calling these functions with actual values provided inside those parenthesis `( )`, those values are referred to as arguments (or actual parameters).

Here's an example where we define a parameter within our greeting:

```python
def personalized_greet(name):
    print(f"Hello there {name}!")
```

Now when calling this function:

```python
personalized_greet("Alice")
```

The output would be:
 
 ```
 Hello there Alice!
 ```

The value `"Alice"` passed into `personalized_greet()` is an argument corresponding to the parameter `name`.

### Return Values

Sometimes instead of just performing actions internally (like printing), functions calculate something and then give back results; they return something back using the keyword 'return'.

For instance,

```python
def add(a,b):
    return a + b
```
 
If you call this addition-function with two numbers,

 ```python 
 result = add(3 , 4)
 print(result)
 ```

It would produce:

 ```
 7
 ```

The expression `a + b` evaluates summing up both operands (`3` and `4`) resulting in integer value (`7`). This value gets returned from our 'add' method back into where it was called - here assigned directly into variable 'result'.

Congratulations! You've now learned how defining functions works along with their fundamental concepts including calls/invocations returning data back from them — crucial building blocks towards mastering Python coding!

Remember practice makes perfect – try creating various types on own seeing what different outcomes come about exploring possibilities available via functional approach within programs/scripts developed!

## Function Parameters and Return Values {#params}

Parameters are variables that act as placeholders for the data you can pass to a function. When defining a function, you specify what kind of information it requires to perform its task. This specification is done through parameters.

Here's an example with one parameter:

```python
def greet(name):
    print(f"Hello, {name}!")
```

The `name` inside the parentheses of `greet(name)` is a parameter – it means that when you call `greet`, you need to provide a name for it to work correctly.

You can also have multiple parameters:

```python
def multiply(x, y):
    result = x * y
    return result
```

In this case, `x` and `y` are both parameters required by the multiply function to perform its calculation.

### Default Parameter Values

Sometimes we want our functions to have default values for certain parameters. In Python, we can assign these defaults using the assignment operator (`=`) within our function definition:

```python
def greet(name="World"):
    print(f"Hello, {name}!")
```

Now if someone calls `greet()` without any arguments like so:

```python
greet()
```

It will output "Hello, World!" because "World" is the default value assigned to name.

### Keyword Arguments

When calling functions with multiple parameters, you might sometimes want to specify them out-of-order or only some of them (assuming others have default values). You do this using keyword arguments where each argument passed has a 'key' matching one of the parameter names in your definition:

```python
def describe_pet(animal_type='dog', pet_name):
    print(f"I have a {animal_type} named {pet_name}.")
    
describe_pet(pet_name='Willie')
```
 
Note: All non-default (required) parameters must come before any default ones in your definitions!

### The Return Statement

Functions don't just execute tasks—they often compute something and then give back results; they return these results using the keyword 'return'. A return statement ends your function execution immediately and sends back whatever follows it as an outcome from running said method/function.

Consider this example:
 
 ```python 
 def subtract(a,b):
     difference = a - b  
     return difference   
 ```

If called,

 ```python 
 print(subtract(10 , 5))
 ```
This would output:
 ```
 5  
 ```

The expression within subtract calculates subtraction between numbers given (`10 - 5`) resulting in integer value (`5`). That value gets returned from our 'subtract' method back into where it was called—in this case printed directly out onto screen/console via built-in 'print()' functionality provided by language itself!

Remember: If no explicit return statement is used or if simply ‘return’ is written without anything following it then Python implicitly returns None meaning absence any particular value whatsoever! 

By mastering how use both input (parameters) alongside outputs ('returns'), developers gain significant control over their code enabling creation much more dynamic & responsive applications capable dealing wide variety scenarios encountered during development process—truly unlocking potential held within programming paradigm itself!

## Variable Scope {#scope}

The "scope" of a variable refers to the region of your program in which that variable is recognized. Variables are only available inside the region they are created, which is determined by where you declare them.

There are two main types of scopes:

- **Local Scope**: A local scope refers to variables defined within a function. These variables are only accessible from within the function they're declared and cannot be used outside of that function.
  
- **Global Scope**: A global scope refers to variables defined at the top level of your script or module or explicitly declared as global using `global` keyword. These variables can be accessed from anywhere in your code.

### Local Variables

When you create a variable inside a function, it's called a local variable. Its scope is limited to that particular function:

```python
def my_function():
    local_variable = 10
    print(local_variable)

my_function()  # This will print: 10
print(local_variable)  # This will raise an error because 'local_variable' is not defined outside 'my_function'
```

As seen above, trying to access `local_variable` outside its defining function results in an error since it doesn't exist there—it's out-of-scope.

### Global Variables

A global variable, on the other hand, has a wider scope and can be accessed both inside and outside functions:

```python
global_variable = "I am global"

def read_global():
    print(global_variable)  # This will work fine and output: I am global
    
read_global()
print(global_variable)  # Also works fine when printed directly.
```

Both calls to `print()` successfully access `global_variable`.

### The `global` Keyword

Sometimes you might want to modify a global variable from within a function; this requires telling Python explicitly that you mean the globally scoped version using the `global` keyword:

```python
counter = 0   # A global counter 

def increment_counter():
    global counter   # Tell Python we want to use the globally scoped 'counter'
    counter += 1     # Incrementing should now affect 'counter' at its highest (global) level
   
increment_counter()
print(counter)   // Outputs: 1 
```

Without declaring `counter` as `global`, attempting modification would result instead creation new separate locally-scoped one—leaving original untouched!

### Nonlocal Variables

In nested functions (functions inside other functions), if we need to modify non-global but also non-local variables (variables not belonging either current innermost enclosing nor outermost/global scopes), then use ‘nonlocal’ keyword indicating such intent:

```python
def outer_func():
    outer_var = "I'm outside!"

    def inner_func():
        nonlocal outer_var   // Now referring specifically previous layer's ‘outer_var’ rather than creating another entirely new one here!
        outer_var = "I've been changed by inner_func!"
    
    inner_func()
    print(outer_var)
   
outer_func()   // Will output: I've been changed by inner_func!
```
Here without usage ‘nonlocal’, again similar situation arises like before potentially causing confusion amongst different layers scoping hierarchy present application structure!

Understanding these differences between various levels/sorts scopes plays fundamental role effectively managing data throughout lifespan software projects thus ensuring smooth execution intended tasks without running into unexpected behavior caused mismanagement same!

## Docstrings {#docstrings}

Docstrings are short for "documentation strings." They are an important tool that helps others understand your code more easily. Unlike regular comments (which use `#`), docstrings are retained throughout the runtime of the program. This allows you to access them using various tools and functions like `help()` or `.__doc__`.

### Writing Docstrings

To add a docstring to a Python function, enclose descriptive text within triple quotes at the beginning of your function body:

```python
def greet(name):
    """
    Greets a person with their name.
    
    Parameters:
    name (str): The name of the person to greet.
    
    Returns:
    None
    """
    print(f"Hello there {name}!")
```

This example shows a simple but well-documented function where anyone reading it can understand its purpose immediately.

### Conventions for Docstrings

PEP 257 provides conventions on how multi-line docstrings should be formatted:

1. The first line should always be a short summary of the object’s purpose.
2. If there are more lines following it, they should be separated by an empty line from the summary.
3. More detailed explanations follow after this blank line.

Here's another example demonstrating these principles:

```python
def calculate_area(base, height):
   """
   Calculate area of triangle given base and height
   
   Given two arguments representing base length and height respectively,
   calculates area according to formula: 0.5 * base * height
   
   Parameters:
   base (float): Length of triangle's base
   height (float): Height measured from base up perpendicular point
   
   Returns:
   float: Calculated area value
   """
   
  return 0.5 * base * height 
```

Notice how parameters and return types/values have been described which aids clarity significantly!

### Accessing DocStrings

You can access these documentation strings via built-in methods such as `help()` passing in either direct reference object itself or alternatively through attribute accessor `. __doc__` :

```python 
print(calculate_area.__doc__)
```
or 

```python 
help(calculate_area)
```

Both would display associated 'calculate_area' method's full explanatory text written inside corresponding earlier provided docstring - proving incredibly useful when trying figure out functionality unfamiliar pieces library/external modules etcetera without needing delve into source directly per se!

Remember: Good documentation practices make maintenance easier not just yourself future self might thank you taking time do so properly now also any other developers come along later down road working same project alongside or even after leave!

[Chapter 3]({{ site.baseurl }}{% link books/python/for-newbies/chapter-03.md %}) \|
[TOC]({{ site.baseurl }}{% link books/python/for-newbies/index.md %})
