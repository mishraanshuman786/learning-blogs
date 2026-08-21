<!-- python basics -->

# Variables and data types in python

To declare variables in Python, you assign a value to an identifier with the assignment `(=)` operator. You don't need to use special keywords like `let` or `const` in JavaScript, or `char` in C#.

```
name = 'John Doe'
age = 25
```

When naming variables in Python, there are some important rules you should keep in mind:

Variable names can only start with a letter or an underscore `(_)`, not a number.
Variable names can only contain alphanumeric characters `(a-z, A-Z, 0-9)` and underscores `(_)`.
Variable names are case-sensitive: `age`, `Age`, and `AGE` are all considered unique.
Variable names cannot be one of Python's reserved keywords such as `if`, `class`, or `def`.
If you break any of those rules, your Python program will raise a `SyntaxError`:

```
 5variable_name = 5
     ^
SyntaxError: invalid syntax
```

First, variable names should be in lowercase, with words separated by an underscore. This is called snake case:
```
my_variable_name = 'freeCodeCamp'
```

## comments in python
In Python, comments start with a pound symbol `(#)`, and the language ignores everything after the # symbol on that line:
```
# This is a single-line comment
```
Multi-line comments can be created by using consecutive single-line comments:
```
# This is a
# multi-line
# comment
```

## Print function
In Python, you can use the `print` function to print data to the terminal.

```
print('Hello world!') # Hello world!
```

You can also use the  `print` function to show multiple values, or arguments, at once by separating them with commas. For example:
```
print('My favorite colors are', 'blue', 'green', 'red')

# Output: My favorite colors are blue green red
```

Python automatically adds a space between each item when you separate them with commas. This is helpful when you want to print several pieces of information together.

## Common data types in python

A data type describes the kind of value a variable holds, for example, a number, a piece of text, or a list of items. Programming languages use data types so they know how to store and work with different kinds of information.

Python is a dynamically-typed language like JavaScript, meaning you don't need to explicitly declare types for variables. The language knows what data type a variable is based on what you assign to it.

Here are some examples:
```
name = 'John Doe' # Python knows this is a string
age = 25 # Python knows this is an integer
```

In Python, type errors can reveal themselves during execution, when the program is actually running and using your code.

Compiled languages catch type errors during the compile step, before the program is allowed to run.

Because of this, you might not learn about a type mistake in Python until the program reaches that specific line of code while running.

Here are the most common data types you'll use in Python:

- `Integer`: A whole number without decimals, for example, `10` or `(-5)`.
```
my_integer_var = 10
print('Integer:', my_integer_var) # Integer: 10
```

- `Float`: A number with a decimal point, like `4.41` or `0.4`.
```
my_float_var = 4.50
print('Float:', my_float_var) # Float: 4.5
```
- `String`: A sequence of characters enclosed in single or double quotation marks like `'Hello world!'`.
```
my_string_var = 'hello'
print('String:', my_string_var) # String: hello
```
- `Boolean`: A true or false type, written as True or False.
```
my_boolean_var = True
print('Boolean:', my_boolean_var) # Boolean: True
```

- `Set`: An unordered collection of unique elements, like `{0.5, 4, 'apple'}`.
```
my_set_var = {7, 'hello', 8.5}
print('Set:', my_set_var) # Set: {8.5, 'hello', 7} (order may vary)
```

- `Dictionary`: A collection of key-value pairs enclosed in curly braces, like `{'name': 'John Doe', 'age': 28}`.
```
my_dictionary_var = {'name': 'Alice', 'age': 25}
print('Dictionary:', my_dictionary_var) # Dictionary: {'name': 'Alice', 'age': 25}
```

- `Tuple`: An immutable ordered collection, enclosed in parentheses, like `('apple', 4.5, 7)`.
```
my_tuple_var = (7, 'hello', 8.5)
print('Tuple:', my_tuple_var) # Tuple: (7, 'hello', 8.5)
```

- `Range`: A sequence of numbers, often used in loops, for example, `range(5)`.
```
my_range_var = range(5)
print('Range:', my_range_var) # Range: range(0, 5)
```

- `List`: An ordered collection of elements that supports different data types.
```
my_list_var = [22, 'Hello world', 3.14, True]
print('List:', my_list_var) # List: [22, 'Hello world', 3.14, True]
```

- `None`: A special value that represents the absence of a value.
```
my_none_var = None
print('None:', my_none_var) # None: None
```

## type() and instance() function in python
 As you build out your programs, you will need to learn how to view the type of a variable.

Here is an example variable:
```
developer = 'Devin'
```
To see what type developer is, you can use the `type()` function like this:
```
developer = 'Devin'

print(type(developer)) # <class 'str'>
```
The output of `<class 'str'>` means that `developer` is a string type.

If you fail to provide any arguments to the `type()` function, then you will receive the following error message:
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: type() takes 1 or 3 arguments
```

Here are all of the data types you have learned so far, along with what the type() function prints for each of them:

```
my_integer_var = 10
print(type(my_integer_var))  # <class 'int'>

my_float_var = 4.50
print(type(my_float_var))  # <class 'float'>

my_string_var = 'hello'
print(type(my_string_var))  # <class 'str'>

my_boolean_var = True
print(type(my_boolean_var))  # <class 'bool'>

my_set_var = {7, 'hello', 8.5}
print(type(my_set_var))  # <class 'set'>

my_dictionary_var = {'name': 'Alice', 'age': 25}
print(type(my_dictionary_var))  # <class 'dict'>

my_tuple_var = (7, 'hello', 8.5)
print(type(my_tuple_var))  # <class 'tuple'>

my_range_var = range(5)
print(type(my_range_var))  # <class 'range'>

my_list = [22, 'Hello world', 3.14, True]
print(type(my_list)) # <class 'list'>

my_none_var = None
print(type(my_none_var))  # <class 'NoneType'>
```

If in your program when you need to verify that a particular variable is a specific type before performing operations on it. This is where the `isinstance()` function comes in handy.

Here is an example variable with a string assigned to it:
```
account_balance = '12'
```

If you try to perform mathematical operations like division using the account_balance variable, then you will receive an error message.
```
account_balance = '12'

account_balance / 2

# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# TypeError: unsupported operand type(s) for /: 'str' and 'int'
```

To see if account_balance is an integer, you can check using the isinstance() function like this:
```
account_balance = '12'

isinstance(account_balance, int) # False
```

The `isinstance()` function also allows you to check for multiple types at once.

Here is an example checking if `account_balance` is an `int` or `float`:
```
account_balance = 12
isinstance(account_balance, (int, float)) # True
```
In this example, `account_balance` is an integer so `isinstance()` returns `True`. If `account_balance` were `12.0`, `isinstance()` would still return `True` because you are checking for integers or floats.

# Strings in Python
A string is a sequence of characters surrounded by either single or double quotation marks.

```
my_str_1 = 'Hello'
my_str_2 = "World"
```

If you need a multi-line string, you can use triple double quotes or single quotes:

```
my_str_3 = """Multiline
string"""
my_str_4 = '''Another
multiline
string'''
```
If your string contains either single or double quotation marks, then you have two options:

- Use the opposite kind of quotes. That is, if your string contains single quotes, use double quotes to wrap the string, and vice versa:
```
msg = "It's a sunny day"
quote = 'She said, "Hello World!"'
```

- Escape the single or double quotation mark in the string with a backslash (\). With this method, you can use either single or double quotation marks to wrap the string itself:
```
msg = 'It\'s a sunny day'
quote = "She said, \"Hello!\""
```

### in Operator
Sometimes, you may need to check if a string contains one or more characters. For that, Python provides the `in` operator, which returns a boolean that specifies whether the character or characters exist in the string or not.

Here are some examples:
```
my_str = 'Hello world'

print('Hello' in my_str)  # True
print('hey' in my_str)    # False
print('hi' in my_str)    # False
print('e' in my_str)  # True
print('f' in my_str)  # False
```

### len() function
To get the length of a string we use `len()` method:
```
my_str = 'Hello world'
print(len(my_str))  # 11
```

Each character in a string has a position called an index. 
```
my_str = "Hello world"

print(my_str[0])  # H
print(my_str[6])  # w
```

Negative indexing is also allowed, so you can get the last character of any string with `-1`, the second-to-last character with `-2`, and so on:

```
my_str = 'Hello world'
print(my_str[-1])  # d
print(my_str[-2]) # l
```

Many other programming languages group data types broadly as either primitive or reference types. Primitive types are simple and immutable, meaning they can't be changed once declared. Reference types can hold multiple values, and are either mutable or immutable. But Python doesn't draw a hard line between those two groups. Instead, all data gets treated as objects, and some objects are immutable while others are mutable.

Immutable data types can't be modified or altered once they're declared. You can point their variables at something new, which is called reassignment, but you can't change the original object itself by adding, removing, or replacing any of its elements.

Strings are immutable data types in Python. This means that you can reassign a different string to a variable:
```
greeting = 'hi'
greeting = 'hello'
print(greeting) # hello
```

But direct modification of a string isn't allowed:
```
greeting = 'hi'
greeting[0] = 'H' # TypeError: 'str' object does not support item assignment
```

Examples of other immutable data types in Python are integer, float, boolean, tuple, and range. You'll get to know each of these types in upcoming lessons.

## String concatenation and string interpolation
When working with strings, combining different pieces of text together is a common operation you'll often find yourself dealing with.

### Concatenating Strings
In Python, you can combine multiple strings together with the plus (+) operator. This process is called string concatenation. Here's how to concatenate two strings with the plus operator:

```
my_str_1 = 'Hello'
my_str_2 = "World"

str_plus_str = my_str_1 + ' ' + my_str_2
print(str_plus_str) # Hello World
```

### Repeating Strings
You can also repeat a string by multiplying it with an integer using the `*` operator. The string is repeated the specified number of times:
```
sound = 'ha'
repeated_sound = sound * 3
print(repeated_sound) # hahaha
```

### Concatenating Strings with Numbers
Concatenation only works with strings. If you try to concatenate a string with a number, you'll get a `TypeError`:

```
name = 'John Doe'
age = 26

name_and_age = name + age
print(name_and_age) # TypeError: can only concatenate str (not "int") to str
```
This happens because Python does not automatically convert other data types like integers into strings when you concatenate them. Python requires all elements to be strings before it can concatenate them. To fix that, you can convert the number into a string with the built-in str() function, which returns the string representation of the given object without modifying the original object:

```
name = 'John Doe'
age = 26

name_and_age = name + str(age)
print(name_and_age) # John Doe26
```

You can also use the augmented assignment operator for concatenation. This is represented by a plus and equals sign (+=), and performs both concatenation and assignment in one step. Here's it in action:

```
name = 'John Doe'
age = 26

name_and_age = name  # Start with the name
name_and_age += str(age)  # Append the age as string

print(name_and_age)  # John Doe26
```

###  String Interpolation
The process of inserting variables and expressions into a string is called string interpolation. Python has a category of string called f-strings (short for formatted string literals).

F-strings start with `f` (either lowercase or uppercase) before the quotes, and allow you to embed variables or expressions inside replacement fields indicated by curly braces ({}). Here's an example:

```
name = 'John Doe'
age = 26
name_and_age = f'My name is {name} and I am {age} years old'
print(name_and_age) # My name is John Doe and I am 26 years old

num1 = 5
num2 = 10
print(f'The sum of {num1} and {num2} is {num1 + num2}') # The sum of 5 and 10 is 15
```

Note how you don't need to convert non-string types with the `str()` function. In the example above, the value of the `age`, `num1`, and `num2` variables is converted under the hood into a string during the interpolation process.

## String slicing

In a previous lesson, you learned how each character in a string can be identified by its index (starting from zero), and accessed using the bracket notation:

```
my_str = "Hello world"

print(my_str[0])  # H
print(my_str[6])  # w
print(my_str[-1]) # d
```
String slicing lets you extract a portion of a string or work with only a specific part of it. Here's the basic syntax:

```
string[start:stop]
```
If you want to extract characters from a certain index to another, you just separate the `start` and `stop` indices with a colon:
```
my_str = 'Hello world'
print(my_str[1:4]) # ell
```

Note that the `stop` index is non-inclusive, so `[1:4]` just extracted the characters from index `1`, and up to, but not including, the character at index `4`.

You can also omit the `start` and `stop` indices, and Python will default to `0` or the end of the string, respectively. For example, here's what happens if you omit the `start` index:

```
my_str = 'Hello world'
print(my_str[:7])  # Hello w
```

This extracts everything from index `0` up to (but not including), the character at index `7`. And here's what happens if you omit the `stop` index:

```
my_str = 'Hello world'
print(my_str[8:])  # rld
```
This extracts everything from the character at index `8` until the end of the string.

Note that slicing a string does not modify the original string:
```
my_str = 'Hello world'
print(my_str[8:])  # rld
print(my_str)  # Hello world
```

You can also omit both the start and stop indices, which will extract the whole string:

```
my_str = 'Hello world'
print(my_str[:])  # Hello world
```

Apart from the `start` and `stop` indices, there's also an optional `step` parameter, which is used to specify the increment between each index in the slice.

Here's the syntax for that:
```
string[start:stop:step]
```

In the example below, the slicing starts at index `0`, stops before `11`, and extracts every second character:

```
my_str = 'Hello world'
print(my_str[0:11:2])  # Hlowrd
```

A helpful trick you can do with the `step` parameter is to reverse a string by setting step to -1, and leaving start and stop blank:

```
my_str = 'Hello world'
print(my_str[::-1]) # dlrow olleH
```

## Common String Methods
A method is a function that belongs to a specific object or class.

Python provides a number of built-in methods that you can use to manipulate strings.

### upper()
Returns a new string with all characters converted to uppercase.
```
my_str = 'hello world'

uppercase_my_str = my_str.upper()
print(uppercase_my_str)  # HELLO WORLD
```
### lower()
Returns a new string with all characters converted to lowercase.

```
my_str = 'Hello World'

lowercase_my_str = my_str.lower()
print(lowercase_my_str)  # hello world
```

### strip()
strip(): Returns a new string with the specified leading and trailing characters removed. If no argument is passed it removes leading and trailing whitespace.
```
my_str = '  hello world  '

trimmed_my_str = my_str.strip()
print(trimmed_my_str)  # "hello world"
```
### replace()
replace(old, new): Returns a new string with all occurrences of old replaced by new.
```
my_str = 'hello world'

replaced_my_str = my_str.replace('hello', 'hi')

print(replaced_my_str)  # hi world
```
### split()
split(separator): Splits a string on a specified separator into a list of strings. If no separator is specified, it splits on whitespace.
```
my_str = 'hello world'

split_words = my_str.split()
print(split_words)  # ['hello', 'world']
```
### join()
join(iterable): Joins elements of an iterable into a string with a separator.

```
my_list = ['hello', 'world']

joined_my_str = ' '.join(my_list)
print(joined_my_str)  # hello world
```
### startswith(prefix)
startswith(prefix): Returns a boolean indicating if a string starts with the specified prefix.
Example Code
my_str = 'hello world'

starts_with_hello = my_str.startswith('hello')
print(starts_with_hello)  # True

### endswith(suffix) 
endswith(suffix): Returns a boolean indicating if a string ends with the specified suffix.
```
my_str = 'hello world'

ends_with_world = my_str.endswith('world')
print(ends_with_world)  # True
```
### find(substring)
find(substring): Returns the index of the first occurrence of substring, or -1 if it doesn't find one.
```
my_str = 'hello world'

world_index = my_str.find('world')
print(world_index)  # 6
```
### count(substring)
count(substring): Returns the number of times a substring appears in a string.
```
my_str = 'hello world'

o_count = my_str.count('o')
print(o_count)  # 2
```

### capitalize()
capitalize(): Returns a new string with the first character capitalized and the other characters lowercased.
```
my_str = 'hello world'

capitalized_my_str = my_str.capitalize()
print(capitalized_my_str)  # Hello world
```
### isupper()
isupper(): Returns True if all letters in the string are uppercase and False if not.
```
my_str = 'hello world'

is_all_upper = my_str.isupper()
print(is_all_upper)  # False
```

### islower()
islower(): Returns True if all letters in the string are lowercase and False if not.
```
my_str = 'hello world'

is_all_lower = my_str.islower()
print(is_all_lower)  # True
```

### title()
title(): Returns a new string with the first letter of each word capitalized.
```
my_str = 'hello world'

title_case_my_str = my_str.title()
print(title_case_my_str)  # Hello World
```





