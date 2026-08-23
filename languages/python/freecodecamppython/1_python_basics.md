<!-- python basics -->

# Variables and data types in python

To declare variables in Python, you assign a value to an identifier with the assignment `(=)` operator. You don't need to use special keywords like `let` or `const` in JavaScript, or `char` in C#.

```
name = 'John Doe'
age = 25
```

When naming variables in Python, there are some important rules you should keep in mind:

- Variable names can only start with a letter or an underscore `(_)`, not a number.
- Variable names can only contain alphanumeric characters `(a-z, A-Z, 0-9)` and underscores `(_)`.
- Variable names are case-sensitive: `age`, `Age`, and `AGE` are all considered unique.
- Variable names cannot be one of Python's reserved keywords such as `if`, `class`, or `def`.
- If you break any of those rules, your Python program will raise a `SyntaxError`:

```
 5variable_name = 5
     ^
SyntaxError: invalid syntax
```

First, `variable names` should be in `lowercase`, with `words` separated by an `underscore`. This is called `snake case`:
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

## type() and isinstance() function in python
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

## Assignment: Build an Employee Profile Generator
This helps in practicing working with `strings` and `string slicing`.
```
first_name = 'John'
last_name = 'Doe'
full_name = first_name + ' ' + last_name
address = '123 Main Street'
address += ', Apartment 4B'
employee_age = 28
employee_info = full_name + ' is ' + str(employee_age) + ' years old'
print(employee_info)
experience_years = 5
experience_info = 'Experience: ' + str(experience_years) + ' years'
print(experience_info)
position = 'Data Analyst'
salary = 75000
employee_card = f'Employee: {full_name} | Age: {employee_age} | Position: {position} | Salary: ${salary}'
print(employee_card)
employee_code = 'DEV-2026-JD-001'
department = employee_code[0:3]
print(department)
year_code = employee_code[4:8]
print(year_code)
initials = employee_code[9:11]
print(initials)

```
# Numbers and Mathematical Operations

## How do you work with Integers and Floating Point Numbers?
Integers and floats are the primary numeric data types in Python. With them, you can store numeric data and perform mathematical operations.

Integers are whole numbers without decimal points, either positive or negative:
```
my_int_1 = 56
my_int_2 = -4

print(type(my_int_1)) # <class 'int'>
print(type(my_int_2)) # <class 'int'>
```

Here's how to perform an addition operation with integers:

```
my_int_1 = 56
my_int_2 = 12

sum_ints = my_int_1 + my_int_2
print('Integer Addition:', sum_ints) # Integer Addition: 68
```
Floats are positive or negative numbers with decimal points, like `3.14`, `-0.5`, or `0.0`.
```
my_float_1 = -12.0
my_float_2 = 4.9

print(type(my_float_1)) # <class 'float'>
print(type(my_float_2)) # <class 'float'>
```

Here's an addition operation with floats:

```
my_float_1 = 5.4
my_float_2 = 12.0

float_addition = my_float_1 + my_float_2
print('Float Addition:', float_addition) # Float Addition: 17.4
```

If you add an integer and a float, the result is automatically converted to a float:

```
my_int = 56
my_float = 5.4

sum_int_and_float = my_int + my_float

print(sum_int_and_float) # 61.4
print(type(sum_int_and_float)) # <class 'float'>
```

This is true for other basic arithmetic operations, too, like subtraction, multiplication, and division. If you mix integers and floats, Python will return a float as the result.

The modulo operator `(%) `returns the remainder when the value on the left is divided by the value on the right:
```
my_int_1 = 56
my_int_2 = 12

my_float_1 = 5.4
my_float_2 = 12.0

mod_ints = my_int_1 % my_int_2
mod_floats = my_float_2 % my_float_1

print('Integer Modulo:', mod_ints) # Integer Modulo: 8
print('Float Modulo:', mod_floats) # Float Modulo: 1.1999999999999993
```

Floor division divides two numbers and returns the greatest integer less than or equal to the result. This is done with the double forward slash operator `(//)`:
```
my_int_1 = 56
my_int_2 = 12

my_float_1 = 5.4
my_float_2 = 12.0

floor_div_ints = my_int_1 // my_int_2
floor_div_floats = my_float_2 // my_float_1

print('Integer Floor Division:', floor_div_ints) # Integer Floor Division: 4
print('Float Floor Division:', floor_div_floats) # Float Floor Division: 2
```

`Exponentiation` raises a number to the power of another, and is done with the double asterisk operator (**):
```
my_int_1 = 56
my_int_2 = 12

my_float_1 = 5.4
my_float_2 = 12.0

exp_ints = my_int_1 ** my_int_2
exp_floats = my_float_1 ** my_float_2

print('Integer Exponentiation:', exp_ints) # Integer Exponentiation: 951166013805414055936
print('Float Exponentiation:',  exp_floats) # Float Exponentiation: 614787626.1765089
```

Sometimes, you might notice that the result of an operation involving floats has more decimal digits than expected. For example, the sum` 0.1 + 0.2` equals `0.30000000000000004` instead of `0.3`.

This happens because numbers are stored in binary format, and some fractions cannot be represented exactly in binary. As a result, they are stored as finite approximations, in the same way the fraction `1/3` cannot be represented with a finite number of digits in decimal and is truncated after a certain number of its infinite digits `(0.33333...)`.

This leads to small rounding errors.

Python also provides built-in functions for converting either numeric data or strings into integers or floats.

The  `float()` function returns a floating-point number constructed from the given number:

```
my_int_1 = 56
my_float_1 = float(my_int_1)

print(my_float_1)  # 56.0
print(type(my_float_1))  # <class 'float'>
```

The `int()` function returns an integer constructed from the given number:

```
my_float = 12.92563
my_int = int(my_float)

print(my_int)  # 12
print(type(my_int))  # <class 'int'>
```
Also, you can use the same built-in functions to convert a string into either a float or integer:

```
my_str_int = '45'
my_str_float = '7.8'

converted_int = int(my_str_int)
converted_float = float(my_str_float)

print(converted_int, type(converted_int))  # 45 <class 'int'>
print(converted_float, type(converted_float))  # 7.8 <class 'float'>
```

Here are some other methods Python provides for working with integers and floats.

- `round()`: Rounds a number to the specified number of decimal places. By default this function rounds to the nearest integer, and returns a whole number with no decimal places:
```
my_int_1 = 4.798
my_int_2 = 4.253

rounded_int_1 = round(my_int_1)
rounded_int_2 = round(my_int_2, 1)

print(rounded_int_1) # 5
print(rounded_int_2) # 4.3
```

- `abs()`: returns the absolute value of a number,
```
num = -15

absolute_value = abs(num)
print(absolute_value) # 15
```

- `pow()`: raises a number to the power of another or performs modular exponentiation.

```
result_1 = pow(2, 3)  # Equivalent to 2 ** 3
print(result_1)  # 8

result_2 = pow(2, 3, 5)  # (2 ** 3) % 5
print(result_2)  # 3
```

## How Do Augmented Assignments Work?

Augmented assignment applies an operation to a variable and stores the result back in the same variable, all in one step.

The basic syntax of an augmented assignment looks like this:
```
variable <operator>= value
```
Which is a more efficient way of doing this:
```
variable = variable <operator> value
```
For example, here's an example of using augmented assignment to add `5` to an existing variable:
```
my_var = 10
my_var += 5

print(my_var) # 15
```

And here is the same thing, but without augmented assignment:
```
my_var = 10
my_var = my_var + 5

print(my_var) # 15
```

## Assignment: Buid a Bill Splitor
- Step 1: In this workshop, you will practice working with numbers and mathematical operations to build a bill splitter. This tool will calculate how much each person owes after adding meal costs and a tip.

To start, you need a way to keep track of the total amount as costs are added.

Create a variable named running_total and assign it the value 0.
- Step 2: Next, you need to account for the number of people sharing the bill. Store this value in a variable, as you did in the previous step.

Create a variable named `num_of_friends` and assign it the value of `4`. This will be used later in the workshop to calculate the final split.

- Step 3: Each course has a cost. You need to store these amounts in variables to use them later. Since these amounts include cents, you will use the float type, which is used to represent decimal numbers. Here's an example of a variable with a float value:
```
change = 2.35
```
Create four variables: `appetizers` set to `37.89`, `main_courses` set to `57.34`, `desserts` set to `39.39`, and `drinks` set to `64.21`.

- Step 4: Now that you have stored the individual costs, you can calculate the total.

Recall that the += operator adds a value to an existing variable and updates it at the same time. For example:

```
total = 10
total += 2 + 2 + 1
print(total)  # total is now 15
```

Use the `+=` operator once to add `appetizers`,` main_courses`, `desserts`, and `drinks` to `running_total`.

Finally, use `print()` to display the string `Total bill so far`: followed by a space and the value of `running_total`.

Note: You might notice that the output has more decimal digits than expected. As you learned in a previous lesson, this happens because numbers are stored in binary, and many decimal values cannot be represented exactly in this format, which leads to rounding errors.

- Step 5: The service was excellent, so the group decides to leave a 25% tip. 
To calculate a percentage in Python, you can multiply the total by the decimal equivalent of the percentage.

For example, to find 10% of a value, you would multiply it by `0.10` using the `*` operator:

```
tax = total * 0.10
```
Create a variable named `tip` and assign it the result of multiplying `running_total` by `0.25`.

Finally, use `print()` to display the string `Tip amount:` followed by a space and the value of your `tip` variable.

- Step 6: Now that you have calculated the tip, you need to add it to your `running_total` to find the final bill amount.

Use the `+=` operator to add the value of `tip` to your `running_total`. Finally, use `print()` to display the string `Total with tip:` followed by a space and the value of `running_total`.

- Step 7: With the tip now included, you have the final amount for the entire group. You have to determine how much each person owes by dividing the total bill by the number of friends.

In Python, you use the forward slash `/` to perform division. For example:

```
half = 10 / 2
```
Create a variable named `final_bill` and assign it the result of dividing `running_total` by `num_of_friends`.

Finally, use the `print()` function to display the string `Bill per person:` followed by a space and the value of `final_bill`.

- Step 8: The bill is split, but division often results in long decimal numbers. Since money is typically represented with two decimal places, you should round the final result.

In an earlier lesson, you learned about the `round()` function which takes two arguments: the number you want to round and the number of decimal places to keep. Here's an example:

```
num = 4.815162342
round(num, 3) # 4.815
```
Use the `round()` function to round `final_bill` to two decimal places and assign the result to a new variable named `each_pays`.

Finally, use `print()` to display the string `Each person pays:` followed by a space and your `each_pays` variable.

With that, the bill splitter workshop is complete.

### Solution:
```
running_total = 0

num_of_friends = 4

appetizers = 37.89
main_courses = 57.34
desserts = 39.39
drinks = 64.21

running_total += appetizers + main_courses + desserts + drinks
print('Total bill so far:', running_total)

tip = running_total * 0.25
print('Tip amount:', tip)

running_total += tip
print('Total with tip:', running_total)

final_bill = running_total / num_of_friends
print('Bill per person:', final_bill)


```
