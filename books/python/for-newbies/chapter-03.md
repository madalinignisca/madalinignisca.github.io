---
layout: page
title:  "Chapter 2: Dive Into Data Types and Variables"
last_modified_at: 2024-02-11 19:19
---

## Understanding Variables and Identifiers

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

That covers basics around understanding what role play within context coding up next explore different types come across regularly journey through learning . Happy Coding!


[Chapter 1]({{ site.baseurl }}{% link books/python/for-newbies/chapter-01.md %}) \|
[TOC]({{ site.baseurl }}{% link books/python/for-newbies/index.md %}) \|
[Chapter 3]({{ site.baseurl }}{% link books/python/for-newbies/chapter-01.md %})