At this point, let's dig into the code a bit. The following sections break
down the checking if numbers are prime in Python.

### Solution

```python
#!/usr/bin/env python
import sys
from math import sqrt, ceil


def is_prime(x):
    if (x % 2 == 0 and x is not 2) or (x == 1):
        return False
    return not bool([n for n in range(3, int(ceil(sqrt(x))+1)) if x % n == 0])


def exit_with_error():
    print('Usage: please input a non-negative integer')
    sys.exit(1)


def main(args):
    try:
        x = int(args[0])
        if x <= 0:
            exit_with_error()
        print(is_prime(x))
    except (IndexError,ValueError):
        exit_with_error()


if __name__ == "__main__":
    main(sys.argv[1:])
```

### The Main Function

Breaking down this solution bottom up,

```python
if __name__ == "__main__":
    main(sys.argv[1:])
```

This bit of code checks to see if this is the main module run. If it is, then it calls the main function.
In this case the user input would be a natural number greater than 1.

```python
def main(args):
    try:
        x = int(args[0])
        if x < 0:
            exit_with_error()
        print(is_prime(x))
    except (IndexError,ValueError):
        exit_with_error()
```

The first thing the main function does is it tries to parse the user input.
All the user inputs are passed in the `args` variable as a list. In this example
we only want the first parameter which we expect to be a natural number.

The arg will be a string so we should convert them to an integer first `x = int(args[0])`.
If the integer is less than 0 it's not a valid input so we return an error by calling the
`exit_with_error()` function.

We then call the main part of our program `print(is_prime(x))` which will check if the integer
is prime and print this out on the terminal for the user

Finally we wrap this entire block in a try ... except, and we catch two exceptions: `IndexError`
and `ValueError`. `IndexError` will be thrown if `args` isn't a list, and we try to access `args[0]`.
`ValueError` will be thrown if we try to convert a non-integer string into an integer.
For example if `args[0]` was "a" -> `int("a")`. If any exceptions are raised, then we call
the `exit_with_error()` function.

### Throw Errors

```python
def exit_with_error():
    print('Usage: please input a non-negative integer')
    sys.exit(1)
```

This function prints a message and then exits the script with an error, `sys.exit(1)`.
If any non-zero value is returned then the program didn't complete properly. This function is called
if the user input isn't correct.

### Prime Numbers

```python
def is_prime(x):
    if (x % 2 == 0 and x is not 2) or (x == 1):
        return False
    return not bool([n for n in range(3, int(ceil(sqrt(x))+1)) if x % n == 0])
```

Now onto the main part of the program. This is the function that actually checks if the integer is prime:

```python
if (x % 2 == 0 and x is not 2) or (x == 1):
    return False
```

This part of the code checks if the integer is divisible by 2 (and not equal 2),
if a number can be divided by 2 it cannot be prime however 2 is a prime number.
Or if the integer is 1, it also cannot be prime by definition.

The `%` is called the modulo operator which returns the remainder of a division, for
example `10 % 2 = 0` because 2 divides into 10 five times evenly (`2 * 5  = 10`). However if we had
`11 % 2 = 1` because 2 divides into 11 five times with one remaining (`2 * 5 + 1 = 11`).

This `x % 2 == 0` is used to check if a number is even, because if it can be evenly
divided by 2 it cannot be prime. If integer is not 1 or divisible by two then we
have do a more thorough check.

`return not bool([n for n in range(3, int(ceil(sqrt(x))+1)) if x % n == 0])`

This is an example of list comprehension which is a way to generate
lists in Python (usually as "one-liners").

Lets break this down.

`for n in range(3, int(ceil(sqrt(x))+1))`

This `range(3, int(ceil(sqrt(x))+1))` generates a list of integers from 3 to the ceiling of the
square of the integer + 1. Ok that sounds complicated but lets take a look at an example
if x was 17, `sqrt(17) = 4.12310.....` -> `ceil(4.1231) = 4.0 + 1 = 5.0` then we convert 5.0 to an
integer `int(5.0) = 5`. So if x is 17 the range function looks like
`range(3, 5)` = `[3, 4, 5]`. We can do this because of some clever maths which means we only
have to check factors up to the square root of the `x` (17) to see if it has any other factors
besides itself and 1. So then `for n in range(3, int(ceil(sqrt(x))+1))` will loop through
every number in that list. So n will be `3, 4, 5`. The range starts at 3 because x will always
be divisible by 1 and we already checked if it's divisible by 2.

`[n for n in range(3, int(ceil(sqrt(x))+1))]`

This on it's own would create a list of the values of `n` so if `x` was `17` then the line above
would generate the list `[3, 4, 5]`.

`[n for n in range(3, int(ceil(sqrt(x))+1)) if x % n == 0]`

Taking a look at the whole list comprehension including `if x % n == 0`
means the current `n` is only added to the list if the if statement evaluates to True,
which is this case is true if `n` divides in `x` evenly. This would make `n` a factor of `x`

So taking a look at our example if `x` is 17 then the list to loop though would
be `[3, 4, 5]`. 

1st Iteration

* `n = 3`
* `17 % 3 = 2`
* Current List = `[]`

2nd Iteration

* `n = 4`
* `17 % 4 = 1`
* Current List = `[]`

3rd Iteration

* `n = 5`
* `17 % 5 = 2`
* Current List = `[]`

So the final generated list for `x = 17` would be `[]` since none of the number `3, 4, 5` divide
evenly into `17`.

Taking a look at the entire line
`return not bool([n for n in range(3, int(ceil(sqrt(x))+1)) if x % n == 0])`.
The `bool()` function converts an object into a `True` or `False` boolean value.
The `not bool(...)` then reverses this value, if `bool("a") = True` then `not bool("a") = False`.
Then we return this value `return not bool(...)`. 

Using our `x = 17` example again `[n for n in range(3, int(ceil(sqrt(x))+1)) if x % n == 0]` = `[]`.
So `return not bool([])` = `return not False` = `return True`, so 17 is prime.

The list that gets generated stores all factors of x except 1 and `17`. So if the list is empty `x` must be prime.
If it contains any factors then it cannot be prime.
