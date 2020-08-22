## Learn: Exception Handling In Python

# Exception Handling

Exceptions, which are language features specifically geared towards handling unusual circumstances during the execution of a program. the foremost common use for exceptions is to handle errors that arise during the execution of a program, but they'll even be used effectively for several other purposes. Python provides a comprehensive set of exceptions, and new ones are often defined by users for their own purposes.

# Exception Block 
The basic Python syntax for exception catching and handling is as follows, using the try, except, and sometimes else keywords:

```
try:
    body
except exception_type1 as e1:
    exception_code1
except exception_type2 as e2:
    exception_code2
    .
    .
    .
except:
    default_exception_code
else:
    else_body
finally:
    finally_body
```

## try/except

### Example:
Let us understand the above statements by making a simple command-line guessing game. The game will generate a random number if the user guessed it correctly then the user will win.

```
from random import randint

target = randint(0,100)

while True:
    guess =int(input("Enter your guess between 1-100: "))
    if guess < target:
        print("Too low")
    elif guess > target:
        print("Too high")
    else:
        print("====You Win====")
        break
```

#### Ouput:

```
Enter your guess between 1-100: 8
Too low
Enter your guess between 1-100: 10
Too low
Enter your guess between 1-100: 20
Too low
Enter your guess between 1-100: thirty
Traceback (most recent call last):
  File "test.py", line 6, in <module>
    guess =int(input("Enter your guess between 1-100: "))
ValueError: invalid literal for int() with base 10: 'thirty'
```

When we input string thirty the program raises an error. To handle it, the program finds an exception handler but if none found the program terminates with an error.

**Note** the line `ValueError:` invalid literal …

**ValueError** is the exception type that we have to handle here. And it can be handle using **try/except** block

```
from random import randint

target = randint(0,100)

while True:
    try:
        guess =int(input("Enter your guess between 1-100: "))
        if guess < target:
            print("Too low")
        elif guess > target:
            print("Too high")
        else:
            print("====You Win====")
            break
    except ValueError:
        print("Please enter a number")
```

#### Ouput:

```
Enter your guess between 1-100: 8
Too low
Enter your guess between 1-100: 10
Too low
Enter your guess between 1-100: 20
Too low
Enter your guess between 1-100: thirty
Please enter a number
Enter your guess between 1-100: 30
Too low
```

A try statement is executed by first executing the code in the body part of the statement. If any error is thrown by the try block, if the exception handler is specified for that error the except statement handles it.

If we want to receive the error message. We can use the sys.stderr parameter in the file argument of print.

```
from random import randint
import sys

target = randint(0,100)

while True:
    try:
       body...
    except ValueError as e:
        print(e, file=sys.stderr)
```

#### Output:

```
Enter your guess between 1-100: five
invalid literal for int() with base 10: 'five'
Enter your guess between 1-100: ...
```

## The else Clause

The else clause of a try statement is optional and rarely used. This clause is executed if and only if the body of the try statement executes without throwing any errors.

Continuing our game, we can use the else clause like following way:

```
from random import randint
import sys

target = randint(0,100)

while True:
    try:
        guess =int(input("Enter your guess between 1-100: "))
    except ValueError as e:
        print(e, file=sys.stderr)
    else:
        if guess < target:
            print("Too low")
        elif guess > target:
            print("Too high")
        else:
            print("====You Win====")
            break
```

Running this code provides the same functionality as before, except that it isolates the error-prone int(input(...)) code in the try statement and the `safe` code in the else statement.

## The finally Clause

The finally clause of a try statement is additionally optional and executes after the try, except, and else sections have executed. The finally clause should always be executed before leaving the try/except statement, whether an exception has occurred or not. this can be usually, prefer to close an open file, database connection, etc.

In our game, we can use the final clause in the following way

```
from random import randint
import sys

target = randint(0,100)
attempts = 0
while True:
    try:
        guess =int(input("Enter your guess between 1-100: "))
    except ValueError as e:
        print(e, file=sys.stderr)
    else:
        if guess < target:
            print("Too low")
        elif guess > target:
            print("Too high")
        else:
            print("====You Win====")
            break
    finally:
        attempts += 1
        print(f"Number of attempts: {attempts}")
```

Running this code is similar to before, except that now we can see how many attempts the user has taken, regardless of whether an exception was raised or not

#### Ouput:

```
Enter your guess between 1-100: 50
Too high
Number of attempts: 1
Enter your guess between 1-100: 25
Too low
Number of attempts: 2
Enter your guess between 1-100: 35
Too low
Number of attempts: 3
Enter your guess between 1-100: 40
Too low
Number of attempts: 4
Enter your guess between 1-100: 45
====You Win====
Number of attempts: 5
```

# The built-in Exceptions and Inheritance hierarchy

It’s possible to generate different types of exceptions to reflect the actual cause of the error or exceptional circumstance being reported. [Here](https://docs.python.org/3/library/exceptions.html#exception-hierarchy) are the exceptions that Python 3.8 provides:

The built-in exception classes are arranged into class **hierarchy inheritance**. This is significant because when we specify an exception class in an except statement, any class which is a subclass of the specified class will be caught in addition to the specified class itself.

Let's look at two built-in exception types **IndexError** and **KeyError**

```
>>> ranks = [1,2,3]
>>> ranks[5]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: list index out of range
```

```
>>> grades = {"A+":"8-10","A":"7-7.99","B+":"6-6.99","B":"5.5-5.99"}
>>> grades["F"]
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
KeyError: 'F'

```

#### Let us check the inheritance hierarchy of this exception types
using method resolution order

```
>>> IndexError.mro()
[<class 'IndexError'>, <class 'LookupError'>, <class 'Exception'>, <class 'BaseException'>, <class 'object'>]
>>> KeyError.mro()
[<class 'KeyError'>, <class 'LookupError'>, <class 'Exception'>, <class 'BaseException'>, <class 'object'>]
```
This shows the full exception class hierarchy from the **object**, the root of all class hierarchies, down through **BaseException**, the root of all exceptions, a class called
**Exception**, to **LookupError**, and finally **IndexError**. We can see that KeyError same as IndexError is also a subclass of LookupError. This means that we can catch both IndexError and KeyError using LookupError class.

So, Instead of

```
try:
    ranks = [1,2,3]
    print(ranks[5])
except IndexError:
    print("We Handled IndexError")

try:
    grades={"A+":"8-10","A":"7-7.99","B+":"6-6.99","B":"5.5-5.99"}
    print(grades["F"])
except KeyError:
    print("We Handled KeyError")
```

We can do
```
try:
    ranks = [1,2,3]
    print(ranks[5])
except LookupError:
    print("We Handled IndexError")

try:
    grades={"A+":"8-10","A":"7-7.99","B+":"6-6.99","B":"5.5-5.99"}
    print(grades["F"])       
except LookupError:
    print("We Handled KeyError")
```

# Defining New Exceptions

When our needs are not met with built-in exceptions we can define our own

Consider the below program that computes the height of the right angle triangle for given hypotenuse and base.

```
import math

def find_height(hypotenuse, base):
    height = math.sqrt(hypotenuse ** 2 - base ** 2)
    return height
```

```
>>> find_height(5,3)
4.0
>>> find_height(5,4)
3.0
>>> find_height(4,5)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "C:\Users\Darsh\github\test.py", line 4, in find_height
    height = math.sqrt(hypotenuse ** 2 - base ** 2)
ValueError: math domain error
```

We get ValueError when we find the square root of a negative number.

This is a vague error, to get a more specific error we can define our own exception class:

```
import math

class HypotenuseError(Exception):
    pass

def find_height(hypotenuse, base):
    if(hypotenuse <  base):
        raise HypotenuseError(f"given hypotenuse {hypotenuse} is less than given side {base}, {hypotenuse} < {base}")
    height = math.sqrt(hypotenuse ** 2 - base ** 2)
    return height
```

When defining our own exception, we should use subclass **Exception** rather than **BaseException**. Here the body of the HypotenuseError class definition contains a simple **pass** statement. It's empty. All the functionality we want is **inherited** from **Exception**. This is a fully functioning exception. It inherits complete implementations of *__init__*, *__str__*,and *__repr__*.


