---

title: Reverse a String in Scheme
layout: default
last-modified: 2020-05-02
featured-image:
tags: [scheme, reverse-a-string]
authors:
  - alexandra_woerner

---

Welcome to the [Reverse String](https://sampleprograms.io/projects/reverse-string) in [Scheme](https://sampleprograms.io/languages/scheme) page! Here, you'll find the source code for this program as well as a description of how the program works.

## Current Solution

{% raw %}

```scheme
(define (reverse-string x)
  (list->string (reverse (string->list x))))

(display (reverse-string (list-ref (command-line) 1)))
```

{% endraw %}

[Reverse String](https://sampleprograms.io/projects/reverse-string) in [Scheme](https://sampleprograms.io/languages/scheme) was written by:

- Francisco Peters
- Jeremy Grifski

If you see anything you'd like to change or update, [please consider contributing](https://github.com/TheRenegadeCoder/sample-programs).

**Note**: The solution shown above is the current solution in the Sample Programs repository as of Aug 10 2021 20:06:41. The solution was first committed on May 07 2018 23:12:09. As a result, documentation below may be outdated.

## How to Implement the Solution

This snippet below shows the whole code you need to reverse a string in Scheme:

```scheme
(define(reverse-string x)
  (list->string (reverse (string->list x))))
(display (reverse-string (read-line)))
```

As you can see, we can write a script to reverse a string in three lines of code.
In the following sections, we'll take a look at a breakdown of each of these lines.

### The Function Definition

```scheme
(define (reverse-string x)
```

The keyword *define* binds a function's definition to the specified name. This
keyword is followed by the name of the function and the function's argument. In
this particular case, the argument *x* is the string we want to reverse.

### The Function Body

```scheme
(list->string (reverse (string->list x))))
```

The whole magic happens in the second line. We will go through it step by step
from the inside out, since this makes understanding it easier.

The most inner pair of parentheses calls the conversion of our string *x* to a
list. Then, this list is reversed by calling the function *reverse* which is part
of the standard library. Finally, the reversed list is converted back to a string.
This is also the return value of the function *reverse-string*.

### The Display

```scheme
(display (reverse-string (read-line)))
```

The first thing you see there, is the *display* function. You'll probably remember
it from our Hello World experience, so have a look there, if you need a quick
refresher of what it does.

The argument to this function is the *reverse-string* function defined above. It
receives the input from the command line, which is accessed with the function
*read-line*, as its string argument. *read-line* reads a single line from the
command line and converts it into a string, so it's perfect for our application!

If you replace `(read-line)` with a string, the program prints that string
reversed. To show you an example, the output of
`(display (reverse-string "Hello"))` is *olleh*.


## How to Run the Solution

The quickest way is probably to try use an online Scheme interpreter. Just copy
the code above, drop it into the editor, fill in some input and hit run.

As an alternative, you can download CHICKEN Scheme and a copy of the solution
file from Github. Assuming CHICKEN Scheme is on your path, you can run the
script from a command line with the following command:

```console
csi -s reverse-string.scm
```

This will run the Scheme file which will print out whatever you enter on the
command line.
