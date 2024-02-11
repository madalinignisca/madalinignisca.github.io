---
layout: page
title:  "Chapter 2: Dive Into Data Types and Variables"
date:   2024-02-11 16:16:16
---
- [Understanding Variables and Identifiers]({{ site.baseurl }}#understanding)
- [Numbers]({{ site.baseurl }}#numbers)
- [Strings]({{ site.baseurl }}#strings)
- [Lists]({{ site.baseurl }}#lists)
- [Tuples]({{ site.baseurl }}#tuples)
- [Sets]({{ site.baseurl }}#sets)
- [Dictionaries]({{ site.baseurl }}#dictionaries)
- [Type Conversion]({{ site.baseurl }}#conversion)

## Understanding Variables and Identifiers {#understanding}

Welcome to the world of Python programming! In this subchapter, we'll delve into one of the most fundamental concepts in any programming language: variables and identifiers. By understanding these concepts, you'll be able to start writing your own programs.

### What Are Variables?

In simple terms, a variable is like a storage box in which you can keep data that may change or vary as your program runs. You can think of it as a label you attach to some information so that you can refer back to it later on without having to remember the exact details.

Variables are essential because they allow us to write flexible code; instead of hardcoding values directly into our programs (which would make them rigid and less adaptable), we use variables as placeholders for data that might change each time we run our program.

Here's how you might create a variable in Python:

```python
greeting = "Hello, World!"
```

In this example, `greeting` is the name of our variable, and `"Hello, World!"` is the value assigned to it.

### Rules for Naming Variables - Identifiers

The names given to variables are also known as identifiers. There are some rules and conventions when naming them:

1. **Names must begin with a letter** (`a-z`, `A-Z`) or an underscore (`_`). They cannot start with numbers.
2. **After the first character**, identifiers can contain letters, underscores (`_`), or digits (`0-9`).
3. **Case Sensitivity**: Variable names are case-sensitive in Python. This means `Greeting`, `greeting`, and `GREETING` would all be different variables.
4. **Reserved Words**: You cannot use reserved words (also called keywords) such as `if`, `for`, or `while` as variable names since they have special meanings in Python.
5. **Readability**: It's best practice to give your variables descriptive names that make it clear what data they hold – for instance, using full words separated by underscores like `user_age` rather than abbreviations like 'ua'.

Examples of valid identifier names include:
```python
username = "tech_writer"
counter = 10
_profile_image_url = "http://example.com/image.jpg"
```

And examples of invalid identifier names:
```python
2nd_place = "Silver" # Invalid because it starts with a number
user-name = "admin" # Invalid because hyphens aren't allowed 
class = "first_class" # Invalid because 'class' is a reserved word 
```

Remembering these rules will help prevent errors related from misnaming your variables.

### Mutable vs Immutable Data Types

It's also important at this stage just briefly mention mutability regarding variables:

- Some objects in Python such as lists and dictionaries are mutable meaning their content can be changed after creation.
- Others like integers strings tuples immutable once created contents cannot altered if try modify actually creating new object assigning same name original 

Let’s see an example demonstrating immutability with strings:

```python
message = "Welcome"
print(id(message))  # Let's say id here is 1234567

message += ", User!"
print(id(message))  # The id will now be different e.g., 7654321
```
When we append ", User!" onto our message string even though appears still named haven't altered existing simply made brand new one old discarded garbage collection process computer manages memory usage efficiently possible 

## Numbers in Python {#numbers}

Numbers are one of the most basic data types in any programming language, and Python is no exception. They are used to perform calculations, represent data, and serve as values that can be manipulated within your programs.

### Types of Numbers in Python

Python supports several different numerical types:

1. **Integers (`int`)**: These are whole numbers which can be positive or negative but do not contain a fractional part. For example: `42`, `-19`, `0`.
2. **Floating Point Numbers (`float`)**: Often known simply as floats, these numbers include a decimal point and can represent real numbers (i.e., fractions). Examples include `3.14159`, `-0.001`, `2.0`.
3. **Complex Numbers (`complex`)**: Less commonly used for beginner projects, complex numbers have a real part and an imaginary part (denoted by 'j'). An example would be `4 + 5j`.

Here's how you might define each type in Python:

```python
# Integer
number_of_planets = 8

# Float
pi_approximation = 3.14

# Complex number
quantum_state = 1 + 4j
```

### Basic Arithmetic Operations

You can perform arithmetic with number data types using various operators:

- Addition (`+`)
- Subtraction (`-`)
- Multiplication (`*`)
- Division (`/`)
- Floor division(`//`) - returns the largest integer less than or equal to the result.
- Modulus operator(`%`) - returns the remainder of dividing two numbers.
- Exponentiation(`**`) - raises one number to the power of another.

For instance:

```python
sum_result = 10 + 15       # Equals 25 (int)
difference_result = 50 - 8 # Equals 42 (int)
product_result = -7 * 3    # Equals -21 (int)
division_result = float(16) / float(5)   # Equals 3.2 (float)

floor_division_result = int(16) // int(5)   # Equals floor division result which is also an integer i.e., equals to int(3).
modulus_result = int(22) % int(6)      # Equals modulus operation result which is also an integer i.e., equals to int(4).
exponentiation_result= pow(int(2),int(-10))     # Raises first argument into power second argument then return exponentiation operation result 
```

It's important to note that when performing operations on integers and floats together, Python will typically convert integers to floats automatically so that it doesn't lose precision during division or other similar operations.

### Numeric Functions 

Python provides built-in functions for working with numeric data types such as:
   
```python   
min()            : Returns smallest element sequence collection items passed arguments e.g min([45,-23]) gives output "-23"
max()            : Opposite above function max([45,-23]) gives output "45"
abs()            : Absolute value abs(-99)=99 regardless sign original inputted 
round(number[, ndigits]): Rounds floating-point according specified digits after decimal if provided round(float('12'),ndigit=int('-1')) results "10" because rounded nearest ten without digit parameter just rounds closest whole rounding rules apply here too remember this key concept while coding using python!
pow(x,y): As seen earlier shortcut '**' performs same action raising x yth power e.g pow(int('2'),int('8')) outputs "256"
```

These utilities help manipulate process mathematical computations easily effectively especially beginners who may not yet familiar more advanced libraries like NumPy SciPy dealing scientific computing tasks later stage learning journey!

## Strings in Python {#strings}

Strings are sequences of characters used to store text data in Python. They can include letters, numbers, symbols, and whitespace (spaces, tabs, newlines). In Python programming, strings are created by enclosing a sequence of characters within quotes.

### Creating Strings

You can create strings using single quotes (`'`), double quotes (`"`), or triple quotes (`'''` or `"""`). Triple quotes allow you to write multi-line strings easily.

```python
# Examples of string creation
single_quoted_string = 'Hello'
double_quoted_string = "World"
triple_quoted_string = """This is a 
multi-line string with line breaks."""
```

Regardless of which type of quote you use to create them, all these examples represent valid strings in Python.

### String Operations

Strings support various operations that let you manipulate their content:

- Concatenation: Combining two or more strings into one.
- Repetition: Repeating a string multiple times.
- Indexing: Accessing individual characters in the string.
- Slicing: Extracting parts of the string.

Here's how these operations look in code:

```python
# Concatenation
greeting = single_quoted_string + ", " + double_quoted_string + "!"
print(greeting)  # Output will be 'Hello, World!'

# Repetition
echo = "Echo! " * 3
print(echo)  # Output will be 'Echo! Echo! Echo! '

# Indexing (Note that indexing starts at 0)
first_letter = greeting[0]
print(first_letter)  # Output will be 'H'

# Slicing 
world_slice = greeting[7:-1]  
print(world_slice)   # Output will be 'World'
```

### Immutable Nature of Strings

It's important to remember that strings are immutable. This means once a string is created; it cannot be changed. Any operation on a string creates a new one rather than modifying the original.

For example:
```python
original_str = "Pythn"
corrected_str = original_str[:2] + "o" + original_str[3:]
print(corrected_str)  # Outputs 'Python', but original_str remains unchanged.
```

### Common String Methods 

Python provides many built-in methods for common tasks involving strings:

```python
sample_text= str("Learning Python!")

lowercased= sample_text.lower()       # Converts all characters lowercase e.g., learning python!
uppercased= sample_text.upper()       # Converts uppercase LEARNING PYTHON!
capitalized= sample_text.capitalize()    # Capitalizes first character only Learning python!

stripped_sample= sample_text.strip('L')     # Removes any leading trailing occurrences letter L from provided argument resulting earning python!

replaced_sample= sample_text.replace(str("Python"),str("coding"))    # Replaces word coding instead thus output becomes Learning coding!

split_sample_list= list(sample_text.split())        #[Learning],[Python!] split where space found each element gets own place within list returned result being ["Learning","Python"]

find_position_character=int(sample_text.find("!"))      #-1 if not found otherwise index position located e.g., would return int(16)

is_digit_check=bool(sample_num.isnumeric())         #"False" since contains non-digit elements however true only digits present useful checking input validation purposes before processing numerical data further down line program execution flow control structures loops etcetera...

These just few there many others explore they make handling manipulation much easier efficient compared doing manually through iteration other techniques beginner level coders might attempt initially unaware such functionality exists ready-made out box language itself!
```

## Lists in Python {#lists}

Lists are one of the most versatile data structures in Python. They can hold a collection of items, which might be numbers, strings, or even other lists. Unlike strings, lists are mutable; their contents can change as you add, remove, or modify elements.

### Creating Lists

A list is created by placing all the items (elements) inside square brackets `[]`, separated by commas.

```python
# An empty list
empty_list = []

# A list of integers
numbers_list = [1, 2, 3]

# A mixed data type list
mixed_list = ["Alice", 28, "Developer"]
```

### Basic List Operations

- **Appending**: Add an item to the end of a list.
- **Inserting**: Insert an item at a given position.
- **Removing**: Remove an item from the list.
- **Popping**: Pop off and return an item from the end or at a specified index.
- **Slicing**: Extract parts of a list.

Here's how these operations look in code:

```python
fruits = ["apple", "banana", "cherry"]

# Appending
fruits.append("orange") # Now fruits -> ["apple", "banana", "cherry", "orange"]

# Inserting 
fruits.insert(1,"blueberry") # Inserts 'blueberry' at index 1: fruits -> ["apple","blueberry","banana","cherry","orange"]

# Removing 
fruits.remove("banana") # Removes 'banana': fruits -> ["apple","blueberry","cherry","orange"]

# Popping 
last_fruit= str(fruits.pop())   # Removes and returns last item: 'orange', now fruits ->["apple" ,"blueberry" ,"cherry"]
specified_fruit=str(fruits.pop(int(0)))    # You can also pop specific index e.g., removes 'apple'

# Slicing 
berries_slice=list(fruits[1:])      #[Start_index:end_index] slices from blueberry till end resulting ['blueberry','cherry']
```

### List Comprehensions

List comprehensions provide a concise way to create new lists where each element is the result of some operation applied to each member of another sequence or iterable.

For example:
```python
squares=[int(x)**int(2) for x in range(int(10))]     #[expression loop condition] generates squares numbers up including int('9') thus output would [0 ,1 ,4 ,9 ,16 ,25 ,36 ,49 ,64 ,'81]
```

### Common List Methods 

Python provides several built-in methods that you can use on lists:

```python
my_list=["a",'b',"c",'d']

length=len(my_list)        # len() function gives total length i.e., number elements within it here would give int('4')

sorted_mylist=list(sorted(my_list))       #"sorted()" sorts alphabetically ascending order default unless otherwise specified so becomes ['a','b','c','d']

reversed_mylist=list(reversed(my_list))         #"reversed()" returns iterator reversed version original therefore need cast back into type before using further ['d,'c','b,'a']

index_of_b=int(my_list.index(str('b')))          #"index()" method will search provided value then return first occurrence found case second place hence int('1')

count_a=my_list.count(str('a'))           #'count()' tallies many times particular appears our scenario once thus returning int('1')
```
Understanding how work with manipulate crucial because they used extensively throughout programming especially when dealing multiple pieces related information simultaneously whether processing user input storing results calculations iterations over datasets etcetera... Moving forward next topics explore tuples sets dictionaries continue building your knowledge base become proficient coder no time!

## Tuples in Python {#tuples}

Tuples are another type of data structure in Python that is similar to lists. The key difference is that tuples are immutable, meaning once a tuple is created, its contents cannot be changed. Tuples are defined by enclosing the elements in parentheses `()` instead of square brackets.

### Creating Tuples

You can create a tuple by placing all the items (elements) inside parentheses `()`, separated by commas. A tuple can also be created without using parentheses; this is known as tuple packing.

```python
# An empty tuple
empty_tuple = ()

# A single item tuple (note the comma)
single_item_tuple = ("hello",)

# A multi-item tuple
multi_item_tuple = ("apple", "banana", "cherry")
```

Even though tuples may seem similar to lists, they have different uses due to their immutability and typically contain heterogeneous (different types of) elements.

### Tuple Operations

Since tuples are immutable, you don't have operations like append or remove which modify the existing structure. However, you can perform other operations:

- **Concatenation**: Combining two or more tuples into one.
- **Repetition**: Repeating a tuple multiple times.
- **Indexing**: Accessing individual items in the tuple.
- **Slicing**: Extracting parts of the tuple.

Here's how these operations look with code examples:

```python
tuple1 = (1, 2, 3)
tuple2 = ('a', 'b', 'c')

# Concatenation
concatenated_tuple= str(tuple1 +tuple2) # Now concatenated_tuple -> "(1 ,2 ,3 ,'a' ,'b' ,'c')"

# Repetition 
repeated_tuple=str(tuple1 * int(3))   # repeated_tuple -> "(1 ,2 ,3 ,1 ,2 ,3 ,1 ,"  etc...

# Indexing 
second_element=tuple[0]     # second_element will hold value at index int('0') i.e., 'int(1)' from first example above 

# Slicing 
slice_of_first_two_elements=tuple[:int(2)]    #[start_index:end_index] slices out just first two resulting '(int('1'),int('2'))'
```

### Unpacking Tuples

One powerful feature of tuples is unpacking where variables assigned corresponding values from within same line statement itself:

```python
my_data=("John Doe" ,"johndoe@example.com" ,"555-0123")

(name,email,number)= my_data       #"unpacks" each element respective variable so name would get string "John Doe" email gets johndoe@example.com number ends up holding phone contact info namely string("555 -0123")
```

Unpacking makes it easy to work with functions that return multiple values and for swapping variable values without needing an extra temporary variable.

### Tuple Methods 

Tuples come with very few built-in methods since their content cannot change after creation. Here’s what you typically use:

```python
my_colors=('red','green','blue','green')

count_green=my_colors.count(str('green'))        #'count()' method returns number occurrences specified argument here twice thus outputting int('2')
index_of_blue=int(my_colors.index(str('blue')))      #'index()' searches provided value then gives back position found case third hence returning int('’))
```

## Sets in Python {#sets}

Sets are a collection type that is unordered and mutable. They are used to store unique elements, meaning they automatically filter out duplicate items. Sets can be useful for membership testing, removing duplicates from a sequence, and computing mathematical operations such as intersection, union, difference, and symmetric difference.

### Creating Sets

You create a set by placing all the items (elements) inside curly braces `{}`, separated by commas. Alternatively, you can use the `set()` function to create a set from an iterable like a list or tuple.

```python
# An empty set
empty_set = set()

# A simple set with strings
fruits_set = {"apple", "banana", "cherry"}

# Creating a set from a list to remove duplicates
numbers_list = [1, 2, 2, 3]
unique_numbers_set=set(numbers_list)   # Resulting unique_numbers_set -> {int(1), int(2), int(3)}
```

It's important to note that sets do not maintain any order; therefore the elements may appear in different orders every time you view them or iterate over them.

### Set Operations

- **Adding Elements**: Add single element using `add()` method or multiple elements using `update()`.
- **Removing Elements**: Remove an element using methods like `remove()` which raises an error if the item doesn't exist or `discard()` which does not.
- **Set Algebra**: Perform operations like union (`|`), intersection (`&`), difference (`-`), and symmetric difference (`^`) between sets.

Here's how these operations look in code:

```python
a= {int('1'), int('2'), int('3')}
b= {int('3'), int('4'), int('5')}

# Adding elements 
a.add(int(6))        # Now 'a' -> {int(1),'',int(3)',int(','')

# Removing elements 
b.discard(int())      # Removes 'if exists else nothing happens 

# Union - combining two sets without duplication 
union_ab=a | b         #'union_ab' will contain all unique values both 'a' & hence {'',''}, etc...

# Intersection - common across both sets only 
intersection_ab=a & b       #'intersection_a_b' contains those present thus just ''

difference_a_b=a-b          #'difference_a_b' has left after taking away shared ones i.e., ',''

symmetric_difference_ab=a ^ b    #'symmetric_difference_a_b" combines everything except overlaps resulting ',',''}
```

### Iterating Over Sets

Iterating over sets works similarly iterating other collections but remember since unordered cannot expect particular order during iteration process:

```python
for fruit in fruits_set:
    print(fruit)
```
This loop prints each fruit contained within our earlier defined however due nature might come out differently than expected each run program unless sorted beforehand!

### Common Set Methods 

In addition built-in algebraic-like mentioned above there several other handy methods available including but limited following examples :

```python
my_favorite_colors={"red","green","blue"}

is_green_in=my_favorite_colors.__contains__(str("green"))     #__contains__() checks whether given argument part returns True False accordingly here would yield true since indeed included initial definition point creation phase earlier on 

clear_all=my_favorite_colors.clear()           #clears empties completely leaving behind equivalent empty curly brackets {}

copy_of_favorites=my_favorite_colors.copy()        #creates shallow copy original one maintaining same contents separate object memory wise though changes made either won't affect counterpart vice versa!
```

## Dictionaries in Python {#dictionaries}

Dictionaries are a built-in data type in Python that store collections of items as key-value pairs. They are mutable, which means they can be changed after they have been created. Dictionaries are unordered until Python 3.7, where they were made to maintain insertion order.

### Creating Dictionaries

A dictionary is created by placing a comma-separated sequence of key:value pairs within curly braces `{}`, with the requirement that keys must be unique (within one dictionary).

```python
# An empty dictionary
empty_dict = {}

# A simple dictionary with string keys and integer values
age_dict = {"Alice": 25, "Bob": 28}

# Using dict() constructor to create a dictionary from tuples
color_dict = dict([("red", "#FF0000"), ("green", "#008000"), ("blue", "#0000FF")])
```

Keys can be any immutable type like strings or numbers. Values can be objects of any type: numbers, strings, lists, other dictionaries etc.

### Accessing Dictionary Elements

You access the elements of a dictionary by using square brackets `[]` containing the key or using the `get()` method:

```python
alice_age= age_dict["Alice"]    # Returns int(25), will raise KeyError if 'Alice' does not exist

bob_age= age_dict.get(str("Bob"))   # Also returns int(28), but will return None instead of an error if 'Bob' is not found.
```

### Modifying Dictionaries

- **Adding/Updating**: Assign value to a new key to add it; assign value to existing key to update it.
- **Removing Items**: Use methods like `pop(key)` which removes specified item and returns its value or `del` keyword.

Here's how these operations look in code:

```python
# Adding/updating entries 
age_dict[str("Charlie")] = int(30)       # Adds Charlie:int('30') into our example above 

age_dict.update({"Alice":int(26),"Dan":int(22)})     # Updates Alice's age and adds Dan:int('22')

# Removing items 
removed_age=int(age_dict.pop(str("Bob")))      # Removes Bob from dict returning his age also i.e., int('28')
del age_dic[str("Charlie")]        # Deletes entry for Charlie entirely without returning anything 
```

Remember when you remove items using del there no undo operation so careful ensure really want rid particular element before doing so!

### Iterating Over Dictionaries

When iterating over dictionaries you typically iterate through keys however also possible obtain values directly both simultaneously depending need situation at hand:

```python
for name in age_d.keys():
    print(name)

for ages in ages.values():
    print(age)

for name ,ages each.items():
    print(f"{name} : {ages}")
```
This loops respectively prints out just names then separately followed combination formatted nicely human readability sake!

### Common Dictionary Methods 

Python provides several built-in methods work efficiently including :

```python
items_view=dict(items())           #'items()' returns view object displays list tuple pairings e.g., [("Alice" ,''), ...]
keys_list=list(keys())             #'keys()' gives all present form could casted further usage outside merely viewing purposes too...
values_collection=dict(values())         #'values()' extracts contained similar fashion prior two examples albeit focused solely part pairing relationship between components making whole structure what fundamentally stands basis conceptually speaking anyway...
clear_all_data=dict(clear())            #"clear()" empties completely leaving behind equivalent nothingness void space previously occupied information now gone forever unless saved elsewhere beforehand precautionary measure avoid loss critical potentially irreplaceable dataset(s)!
copy_of_dictionary=dictionary.copy()          #"copy()" creates shallow copy original one maintaining same contents separate object memory wise though changes made either won't affect counterpart vice versa much sets earlier!
```
   
## Type Conversion in Python {#conversion}

Type conversion, also known as type casting, is the process of converting one data type into another. In Python, this can be done using built-in functions that return a new object representing the converted value.

### Implicit Type Conversion

Python automatically converts one data type to another without any user involvement. This is known as implicit type conversion or coercion. It typically happens during arithmetic operations where mixing types may occur.

```python
integer_num = 6          # int
float_num = 1.2          # float

# Adding an integer and float results in a float implicitly
result = integer_num + float_num  
print(result)            # Output: 7.2 (float)
```

In the example above, `integer_num` was implicitly converted to a `float` when added to `float_num`.

### Explicit Type Conversion

Explicit type conversion requires manually converting from one type to another using specific functions:

- **int()**: Converts an object to an integer.
- **float()**: Converts an object to a floating-point number.
- **str()**: Converts an object to a string representation.
- **list()**: Converts an iterable (like tuples, sets, dictionaries) into a list.
- **tuple()**: Converts an iterable into a tuple.
- **set()**: Converts an iterable into a set which removes duplicates and sorts it in ascending order until specified otherwise.

Here are some examples demonstrating explicit conversions:

```python
num_string = "123"       # String containing numerical digits

# Converting string to integer 
converted_int=int(num_string)    # Now 'converted_int' -> int(123)

# Converting string to float 
converted_float=float(num_string)   # Now 'converted_float' -> float(123.0)

# Converting number back into string 
back_to_str=str(converted_int)      #'back_to_str' will now hold "int('123')"

# Convert list into tuple 
sample_list=[1,'a',True]
tuple_from_list=tuple(sample_list)     #'tuple_from_list' -> (int(1),'a',True)

# Convert tuple back into list so we can modify it later if needed since tuples immutable!
list_from_tuple=list(tuple_from_list)
```

### Handling Value Errors During Conversion 

Not all objects can be converted between types; attempting such conversions might raise errors like `ValueError`. Always ensure that you're performing sensible conversions:

```python
try:
    invalid_conversion=int("abc")     #"abc" cannot be interpreted as integer hence ValueError exception raised caught block below...
except ValueError:
    print("Cannot convert non-numerical strings integers!")
```
It's good practice use try-except blocks handle potential exceptions gracefully especially dealing with input could vary widely terms format content being passed through various parts program runtime!

## Thoughts

Understanding how why perform necessary foundational skill develop early stages learning programming languages particularly ones dynamic typing system place python where certain amount flexibility allowed encouraged even though comes risks associated incorrect usage thereof! Moving forward next chapters explore more complex concepts continue build upon solid base knowledge acquired thus far journey becoming proficient coder awaits ahead...

[Chapter 1]({{ site.baseurl }}{% link books/python/for-newbies/chapter-01.md %}) \|
[TOC]({{ site.baseurl }}{% link books/python/for-newbies/index.md %})