According to Wikipedia, Pascal is an imperative and procedural language which 
first appeared in 1970. Pascal's creator, Niklaus Wirth, designed the language 
with compiler and runtime efficiency in mind. In addition, Wirth drew much of 
the inspiration for Pascal from the ALGOL family of languages.

That said, Pascal isn't simply an ALGOL clone. In fact, Pascal includes many 
additions to ALGOL such as mechanisms for defining custom datatypes. Likewise, 
the language includes several additional features like enumerations, subranges, 
and records.

As an added bonus, Pascal is a strongly typed language. This forces the user to 
explicitly write conversions between types, so errors can be caught at compile 
time. Unfortunately, I've read that Pascal has a loophole in the type system. I 
just haven't found any articles describing it. If you know, let me know in the 
comments.

Before we get into Hello World, I want to look a bit deeper at sets because I find 
them interesting. In Pascal, we can define a set as follows:

```pascal
var
  Set1 : set of 5..20;
  Set2 : set of 'f'..'m';
```

With Pascal being such an old language, I find it interesting how intuitive the set 
syntax is. In fact, I can't think of many industrial languages that have such a nice 
syntax for setting up lists or sets. In fact, here's how you would generate a list of 
numbers in a few languages:

```java
// Java 8+
int[] range = IntStream.rangeClosed(5, 20).toArray();
```

```python
# Python 3
list(range(5, 20))
```

```javascript
// JavaScript
var list = [];
for (var i = 5; i <= 20; i++) {
  list.push(i);
}
```

```c#
// C#
int[] values = Enumerable.Range(5, 15).ToArray();
```

That Pascal set syntax is great. In fact, it even allows us to do fun things like 
check values in some range:

```pascal
if i in [5..20] then
```

At any rate, I think we've played around enough
