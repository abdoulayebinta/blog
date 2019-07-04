---
layout: post
title:  "Debugging and Error Handling in Python"
author: abdoulaye
categories: [ development ]
image: assets/images/python-exception.jpg
hidden: false
---
- Explain common errors and how they occur in Python
- Use pdb to set breakpoint and step through code
- Use try and except blocks to handle errors

## Common Types of Error in Python 

You're going to make mistakes...

So how do you fix them ?

Understand them!

Let's start with some common errors!

## SyntaxError 

- Occurs when Python encounters incorrect syntax
(something it doesn't parse)

- Usually due to typos or not knowing Python well enough

```python 
def first: # SyntaxError
None = 1  # SyntaxError
return   # SyntaxError
```

## NameError

This occur when a variable is not defined, i.e it hasn't been
assigned

```python 
test
# NameError: name 'test' is not d efined
```

## TypeError 
>Occurs when: 
>- An operation or function is applied to the wrong type
>- Python cannot interpret an operation on two data types

```python
len(5)
# TypeError: object of type 'int' has no len()
"Abdoulaye" + []
# TypeError: must be str, not list
```

## IndexError
>Occurs when you try to access an element in a list using an 
invalid index(i.e one that is outside the range of the list or string):

```python
name = "Bah"
name[0]  # B
name[3]  # IndexError: string index out of range
nums = (1,2,3,4)
nums[6]  # IndexError: tuple index out of range
list = ["Bonjour"]
list[2] # IndexError: list index out of range
```

## ValueError
This occurs when a built-in operation or function receives an argument that 
has the right type but an inappropriate value:
```python
int("5")  # 5 --> This is OK
int("houpla")
# ValueError: invalid literal for int() with base 10: 'houpla'
```

## KeyError 

> This occur when a dictionary does not have a specific key: 
```python
d = {}
d["foo"]
# KeyError: 'foo'
```

## Raising our Own Errors
---
### Raise Your Own Exception!
In python we can also throw errors using the raise keyword.
This is helpful when creating your own kinds of exception and error messages.
```python
raise ValueError('invalid value')
# ValueError: invalid value
raise NameError('Abdoulaye')
NameError: Abdoulaye
```
#### Exemple
Let's define a function that takes a text and colorize it
```python 
def colorize(text, color):
    colors = ("cyan", "yellow", "blue", "green", "magenta")
    if type(color) is not str:
        raise TypeError("color must be intance of string")
    if type(text) is not str:
        raise TypeError("text must be instance of string")
    if color not in colors:
        raise ValueError("color is invalid color")
    print(f"Printed {text} in {color}")

colorize("hello", "red")   # ValueError: color is invalid color
colorize("hi", 10)         # TypeError: color must be instance of string
colorize(34, "green")      # TypeError: text must be isntance of string
```


## Try and Except Blocks
### Handle Errors!
In Python, it is **strongly** encouraged to use try/except blocks, to catch exceptions when we can do something about them. Let's see what that looks like.
```python
d = {"name": "Bah"}
d["city"]   # KeyError: 'city'

def get(d, key):
    try: 
        return d[key]
    except KeyError:
        return None

print(get(d, "name")) # Bah
print(get(d, "city")) # None
```

## Try Except Else and Finally

Capture user input as a number and throw erros if it's not a number
```python 
while True:
    try:
        num = int(input("please enter a number: "))
    except: 
        print("That's not a number!")
    else: 
        print("Good job, you entered a number!")
        break
    finally:
        print("Runs no matter what!")
```

```python
def divide(a, b):
    try: 
        result = a/b
    except (ZeroDivisionError, TypeError) as err:
        print("Something went wrong!")
        print(err)
    else:
        print(f"{a} divided by {b} is {result})
```

## Debugging with PDB

```python
def add_numbers(a, b, c, d):
    # importing the python debugger
    import pdb; pdb.set_trace()

    return a + b + c + d

add_numbers(1,2,3,4)
``` 
### Common PDB Commands
- l (list)
- n (next line)
- p (print)
- c (continue - finishes debugging)