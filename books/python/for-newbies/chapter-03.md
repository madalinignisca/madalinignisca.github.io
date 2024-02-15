---
layout: page
title:  "Chapter 3: Controlling the Flow – Making Decisions and Repeating Actions"
last_modified_at: 2024-02-12 12:12
---
- [Conditional Statements]({{ site.baseurl }}#statements)
- [The while loop]({{ site.baseurl }}#while)
- [Mastering for loops]({{ site.baseurl }}#for)
- [Exploring the range() Function]({{ site.baseurl }}#range)
- [Managing Loop Execution with break, continue, and pass]({{ site.baseurl }}#break)
- [Introducing Pattern Matching With match]({{ site.baseurl }}#match)

## Conditional Statements {#statements}

Conditional statements are a fundamental part of programming, allowing your code to make decisions based on certain conditions. In Python, these decisions can be made using `if`, `elif` (which stands for 'else if'), and `else` statements.

**Understanding if Statements**

An `if` statement is used to test a condition and execute a block of code only if that condition is true. Here's the basic syntax:

```python
if condition:
    # Block of code executed if the condition is True
```

For example:

```python
age = 20
if age >= 18:
    print("You are an adult.")
```

In this case, because age is greater than or equal to 18, the message "You are an adult." will be printed.

**Handling Multiple Conditions with elif**

Sometimes you need to check multiple conditions in sequence; this is where `elif` comes into play. If the initial `if` statement evaluates to False, Python moves on to evaluate any subsequent `elif` blocks.

Here's how it works:

```python
temperature = 30

if temperature < 0:
    print("It's freezing!")
elif temperature < 20:
    print("It's cold")
elif temperature < 30:
    print("It's warm")
else:
    print("Wow! It's hot!")
```

Since our temperature variable equals 30, "Wow! It’s hot!" will be printed out.

**Using else for Alternative Actions**

If none of the conditions specified by your `if` and/or `elif` statements are met, you can use an optional final clause called else:

```python
number = -2

if number > 0:
    print(f"{number} is positive.")
elif number == 0:
    print(f"The number is zero.")
else: 
  	print(f"{number} is negative.")
```

The output here would be "-2 is negative."

Remember that after Python finds one true condition in your series of if/elif/else clauses, it executes that block alone and skips all others—so order matters!

## The while loop {#while}

The `while` loop in Python enables you to execute a block of code repeatedly as long as a condition is true. It's an essential tool for when you want to continue performing an action until a particular state changes.

**Creating a while loop**

Here’s the basic structure of a `while` loop:

```python
while condition:
    # Block of code executed repeatedly 
    # as long as the condition is True
```

For example, if we wanted to count from 1 to 5, we could write:

```python
count = 1
while count <= 5:
    print(count)
    count += 1   # This is shorthand for count = count + 1
```

This will output numbers from 1 through 5. The loop continues running until `count` becomes greater than five.

**Infinite Loops and How to Avoid Them**

An infinite loop occurs when the terminating condition never becomes false. To avoid this, ensure that the variable used in the condition statement changes within each iteration so it can eventually become false.

For instance, forgetting to include `count += 1` in our previous example would result in an infinite loop because `count` would always remain at its initial value (which is less than or equal to five).

Always double-check your loops' logic and conditions before running them!

**Combining while Loops with Conditional Statements**

You can make more complex decisions by combining conditional statements inside your `while` loops:

```python
user_input = ""
while user_input.lower() != "quit":
    user_input = input("Enter 'quit' to exit: ")
print("Thank you! Exiting program.")
```

In this script, users are prompted continuously until they type "quit" (case insensitive due to `.lower()`), at which point the program prints out a farewell message and stops executing.

Through careful use of conditions within your loops, you can control not only how many times those loops run but also under what circumstances they terminate or continue—giving you precise control over your programs’ behavior.

## Mastering for loops {#for}

The `for` loop in Python is a versatile control structure that allows you to iterate over the elements of a sequence (such as a list, tuple, string, or range) and execute a block of code for each element.

**Iterating Over Sequences with for loops**

A basic `for` loop looks like this:

```python
for item in sequence:
    # Block of code to execute for each item
```

For example, if we want to print out each character in a string one by one:

```python
for character in "Python":
    print(character)
```

This will output:
```
P
y
t
h
o
n
```

You can also iterate through lists and other iterable objects using the same syntax.

**Nested for loops**

Sometimes you need to use one loop inside another; these are called nested loops. For instance, if you're going to process every cell in a grid represented by rows and columns:

```python
rows = 3 
columns = 4 

for row_num in range(rows):
    for col_num in range(columns):
        print(f"Row {row_num}, Column {col_num}")
```

This script would produce an output that shows the row and column index of each cell position within our grid.

Be cautious when nesting loops since it's easy to create scripts that take much longer than expected due to their multiplying effect on execution time—this is known as quadratic runtime complexity (O(n²)).

By mastering both simple and nested `for` loops, you'll be able to handle many common tasks involving repeated actions across data structures—a fundamental skill for any Python programmer.

## Exploring the range() function {#range}

The `range()` function is a built-in Python function that generates a sequence of numbers. It is often used for looping a specific number of times in `for` loops.

**Generating Number Sequences with range()**

Here's how you can use the `range()` function:

```python
# Using range to generate numbers from 0 up to (but not including) 5
for i in range(5):
    print(i)
```

This will output:
```
0
1
2
3
4
```

The `range()` function by default starts at zero and increments by one each time, but you can customize it further.

**Using range() in Loops**

You can specify both start and end points for your sequences as well as a step value:

```python
# Starting at 1, ending before 10, stepping by two each time.
for i in range(1, 10, 2):
    print(i)
```

This loop will print out odd numbers between one and ten:
```
1
3
5 
7 
9 
```

It’s important to note that the starting index is inclusive while the ending index is exclusive; meaning that Python includes the first value but stops before reaching the last value specified.

## Managing Loop Execution with break, continue, and pass {#break}

In Python loops, you have control statements such as `break`, `continue`, and `pass` that change the flow of your iterations in different ways. These can be used within both `for` and `while` loops.

**Stopping a Loop Prematurely with break**

The `break` statement is used to exit a loop before it has gone through all its iterations:

```python
# Print numbers until we reach a number divisible by 7
for number in range(1, 100):
    if number % 7 == 0:
        print(f"{number} is divisible by 7.")
        break   # Exit the loop
```

When this code runs, it will stop at the first number divisible by seven (which is seven) and then terminate the loop.

**Skipping Iterations with continue**

Unlike `break`, which exits the loop entirely, the `continue` statement skips over the current iteration and moves on to the next one:

```python
# Skip even numbers and only print odd ones between 1-10.
for number in range(1,11):
    if number % 2 == 0:
        continue   # Skip this iteration
    print(number)
```

This script prints out only odd numbers because whenever an even number is encountered (`number % 2 == 0`), it triggers a continue statement that skips to the next iteration without executing any further code below it for that cycle.

**Placeholder Behavior of pass**

The final control statement is `pass`. It does nothing—it's simply a placeholder you can use when syntax requires some sort of action or content but you don't want any operation or behavior implemented yet:

```python
# A for-loop where we're not sure what we're doing yet.
for x in range(10):
    pass   # We'll figure out what goes here later.
```

Using 'pass' allows your code to run without interruption while signaling areas where future code may be added. This can be particularly useful during development stages or when implementing stubs.

## Introducing Pattern Matching With match (Python 3.10+) {#match}

Starting with Python version 3.10, a new feature called structural pattern matching was introduced, resembling the switch-case statements found in other programming languages but with more powerful capabilities. This is done using the `match` statement followed by one or more `case` clauses.

**Basic Syntax of match...case Statement**

The basic structure of a `match` statement looks like this:

```python
match subject:
    case pattern1:
        # Block of code executed if subject matches pattern1
    case pattern2:
        # Block of code executed if subject matches pattern2
    ...
```

Here's an example that demonstrates how to use it:

```python
def http_status_code(status):
    match status:
        case 200 | 201 | 202:   # You can match multiple patterns.
            return "Success"
        case 404:
            return "Not Found"
        case _:
            return "Other"

print(http_status_code(200))   # Output: Success
print(http_status_code(404))   # Output: Not Found
print(http_status_code(500))   # Output: Other

```

In this function, we're matching the HTTP status codes and returning appropriate messages for each group of statuses.

**Note**: The last line uses `_`, which acts as a wildcard and will match anything not previously matched by earlier cases.

Pattern matching is especially useful when you have complex data structures such as nested lists or dictionaries because you can destructure them directly within your patterns:

```python
point = (0, -1)
match point:
    case (0, y) if y > 0:
        print("Point lies on positive Y axis")
    case (0, y) if y < 0:
        print("Point lies on negative Y axis")
    case _ :
        print("Point does not lie on Y axis")

# Since our point variable has coordinates (0,-1), 
# it would output "Point lies on negative Y axis".
```

This advanced form of control flow allows for concise and readable conditions that are particularly handy when dealing with various possibilities that could arise from your program’s data.

Please note that while `match` statements offer powerful functionality for handling complex conditionals gracefully, they should be used judiciously—especially for beginners—as they introduce another layer of complexity to understanding program flow.

[Chapter 2]({{ site.baseurl }}{% link books/python/for-newbies/chapter-02.md %}) \|
[TOC]({{ site.baseurl }}{% link books/python/for-newbies/index.md %}) \|
[Chapter 4]({{ site.baseurl }}{% link books/python/for-newbies/chapter-04.md %})
