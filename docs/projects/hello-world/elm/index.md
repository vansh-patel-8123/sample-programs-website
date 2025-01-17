---

title: Hello World in Elm
layout: default
last-modified: 2020-05-02
featured-image: hello-world-in-elm-featured-image.JPEG
tags: [elm, hello-world]
authors:
  - the_renegade_coder

---

Welcome to the [Hello World](https://sampleprograms.io/projects/hello-world) in [Elm](https://sampleprograms.io/languages/elm) page! Here, you'll find the source code for this program as well as a description of how the program works.

## Current Solution

{% raw %}

```elm
module HelloWorld exposing (..)

import Html exposing (text)

main =
  text "Hello, World!"
```

{% endraw %}

[Hello World](https://sampleprograms.io/projects/hello-world) in [Elm](https://sampleprograms.io/languages/elm) was written by:

- Jeremy Griffith

If you see anything you'd like to change or update, [please consider contributing](https://github.com/TheRenegadeCoder/sample-programs).

**Note**: The solution shown above is the current solution in the Sample Programs repository as of Apr 19 2018 18:37:30. The solution was first committed on Apr 11 2018 12:33:24. As a result, documentation below may be outdated.

## How to Implement the Solution

As usual, let's dive right into the implementation of 
Hello World in Elm:

```elm
module HelloWorld exposing (..)
import Html exposing (text)
main =
  text "Hello, World!"
```

And, that's it! We can write Hello World in Elm in just 
a few lines of code, but what's really going on in this 
code?

Up first, we have the module declaration line. In other 
words, we've defined a module with the name HelloWorld. 
If anyone wanted to use this module, everything would be 
completely exposed.

In the third line, we import the Html module, so we can 
access the text functionality. As we can probably imagine, 
the text function just displays text to the user.

Finally, as with many functional languages, we have the 
main function. To no surprise, the main function is a 
special function which provides the starting point for 
the program. In the case of Elm, the main function must 
retain an element to draw into the page. In our case, we're 
returning a HTML element from the text function.


## How to Run the Solution

Okay, so we have a solution, but how do we run it? Well, 
Elm is a bit different than our typical languages because 
it's for web use only. As a result, we'll want to download 
the necessary utilities first.

Now would be a good time to install Elm. With that installed, 
get the Html package from the command line:

```shell
elm-package install elm-lang/html
```

After that, grab a copy of the elm solution from GitHub. Now, 
in the same folder as the new file, run the following from the 
command line:

```shell
elm reactor
```

This will basically launch a local server for testing. Now, go 
to the local server location in a browser and open the HelloWorld 
file. That's it!

Alternatively, use an online Elm compiler for testing code snippets. 
Give it a go!
