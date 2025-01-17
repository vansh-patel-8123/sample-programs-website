---

title: Hello World in Elixir
layout: default
last-modified: 2020-05-02
featured-image: hello-world-in-elixir-featured-image.JPEG
tags: [elixir, hello-world]
authors:
  - the_renegade_coder

---

Welcome to the [Hello World](https://sampleprograms.io/projects/hello-world) in [Elixir](https://sampleprograms.io/languages/elixir) page! Here, you'll find the source code for this program as well as a description of how the program works.

## Current Solution

{% raw %}

```elixir
IO.puts "Hello, World!"
```

{% endraw %}

[Hello World](https://sampleprograms.io/projects/hello-world) in [Elixir](https://sampleprograms.io/languages/elixir) was written by:

- Jeremy Grifski

If you see anything you'd like to change or update, [please consider contributing](https://github.com/TheRenegadeCoder/sample-programs).

## How to Implement the Solution

Alright, let's get right to it:

```elixir
IO.puts "Hello, World!"
```

As we can see, Hello World in Elixir is just a single line of 
code. As usual, let's dig into it a bit.

Up first, we have a reference to the IO module. In Elixir, the IO 
module is the standard tool for working with standard input and 
output as well as files and other devices. So, it makes sense that 
we'd use it here to gain access to standard output.

Up next, we call the puts function of the IO module. Like print in 
most languages, puts simply writes a value to standard output. In 
fact, we aren't limited to standard output. We can redirect the output 
to other streams such as standard error:

```elixir
IO.puts :stderr, "Uh Oh!"
```

At any rate, puts, in our primary example, will simply write "Hello, 
World!" to the user. To be honest, I'm surprised this is only the 
second time we've seen the puts keyword in this series, the first being 
Ruby.


## How to Run the Solution

As always, if we want to give the code above a try, we can use an online 
Elixir editor. Copy the code into the editor and hit run.

Alternatively, we can run the solution locally if we download the latest 
version of Elixir. After that, we'll want to get a copy of the solution. 
Assuming Elixir is in our path, all we have to do is run the following 
commands from the command line:

```shell
elixir hello-world.ex
```

If successful, the "Hello, World" string should print to the console.
