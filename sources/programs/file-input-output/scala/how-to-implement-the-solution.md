First of all let's look at the read / write functions as a whole, and their usages:

```scala
import scala.io.Source
import java.io.{FileNotFoundException, IOException, File, FileOutputStream, PrintWriter}

object FileIO {
{
  // reading file then write to stdout
  // write exception when fail
  def readFromFile(filename: String) {
    try {
      val buffer = Source.fromFile(filename)
      val lines = buffer.getLines

      lines.foreach(println)
      buffer.close
    } catch {
      case e: FileNotFoundException => println(s"File ${filename} does not exist.")
      case e: IOException => println(s"I/O Exception when reading from ${filename}.")
      case e: Throwable => println(s"Error ${e.getMessage} when reading from ${filename}.")
    }
  }

  // reading file into Option type using generators
  // fail silently
  def readFromFileIntoOption(filename: String): Option[List[String]] = {
    try {
      val buffer = Source.fromFile(filename)
      val lines = (
        for (line <- buffer.getLines)
          yield line
        ).toList

      buffer.close
      Some(lines)
    } catch {
      // any exception will results to None
      case e: Exception => None
    }
  }

  // write to file
  // stdout exception when fail
  def writeToFile(filename: String, contents: String) {
    try {
      val writer = new PrintWriter(new File(filename))
      writer.write(contents)
      writer.close
    } catch {
      case e: FileNotFoundException => println(s"Cannot write into file ${filename}.")
      case e: Throwable => println(s"Error ${e.getMessage} when writing to file ${filename}.")
    }
  }

  // using Option to wrap writing to file
  // with this method, if we can't write to file, nothing will be executed
  def optionWriteToFile(filename: String, contents: String) {
    val writer: Option[PrintWriter] =
    try {
      Some(new PrintWriter(new File(filename)))
    } catch {
      case e: Exception => None
    }
    writer.foreach { w => w.write(contents); w.close }
  }

  def main(args: Array[String]) {
    // usages:

    // read successfully
    println("readFromFile:")
    readFromFile("input.txt")

    println("readFromFileIntoOption:")
    val lines = readFromFileIntoOption("input.txt")
    lines.map(_.foreach(println))

    // read failing
    println("readFromFile non-exist:")
    readFromFile("non-exist.txt")

    println("readFromFile not-permitted:")
    readFromFile("not-permitted.txt")

    // read silently failing
    println("readFromFileIntoOption non-exist:")
    val optionLines = readFromFileIntoOption("non-exist.txt")
    optionLines.map(_.foreach(println))

    println("readFromFileIntoOption not-permitted:")
    val anotherOptionLines = readFromFileIntoOption("not-permitted.txt")
    anotherOptionLines.map(_.foreach(println))


    // write succesfully
    println("writeToFile:")
    writeToFile("output.txt", "I am a string.\n")

    println("optionWriteToFile:")
    optionWriteToFile("output2.txt", "There another string.\n")

    // write failing
    println("writeToFile not-permitted:")
    writeToFile("not-permitted.txt", "Can I write to this file?")

    // write silently failing
    println("optionWriteToFile not-permitted:")
    optionWriteToFile("not-permitted.txt", "Can I write to this file?")
  }
}
```

### Read from a file

In many real world scenario, your program usually takes one of the two approaches when dealing with undeterministic I/O
(also called side-effects): fail loudly or fail silently.

We want to fail loudly, i.e. throw exception, stop execution flow or output error as results, when the I/O is critical
for the program to proceed.

```scala
// reading file then write to stdout
// write exception when fail
def readFromFile(filename: String) {
  try {
    val buffer = Source.fromFile(filename)
    val lines = buffer.getLines

    lines.foreach(println)
    buffer.close
  } catch {
    case e: FileNotFoundException => println(s"File ${filename} does not exist.")
    case e: IOException => println(s"I/O Exception when reading from ${filename}.")
    case e: Throwable => println(s"Error ${e.getMessage} when reading from ${filename}.")
  }
}
```

Similar to many other language, `scala.io.Source` provides the ability to get a file into a buffer-like instance,
in our case `BufferedSource`, using `fromFile`. `Source` is built-in with `Java` exceptions to let us know what
causes the failure in opening / reading the file.

Since we are dealing with a text file, we can simply use `getLines` to convert `BufferedSource` to a `Iterator[String]`.
We can also convert `Iterator[String]` to a `List[String]` or `Array[String]` using `.toList` and `.toArray`
respectively.

`Iterator` interface allows us to traverse each line, using `foreach`. The syntactic sugar `lines.foreach(println)`
you see here is short-hand for:

```scala
lines.foreach(line => println(line))
```

or

```scala
for (line <- lines) {
  println(line)
}
```

After extracting the buffer, we close it with `buffer.close`.

`catch` block here demonstrate Scala's pattern matching feature. By default, all exceptions can be caught
as a `Throwable`.
However we have the option to deal with specific exception (`FileNotFoundException` or `IOException`) separately.

Usage is simple:

```scala
readFromFile("input.txt")
```

On the other hand, instead of yelling at the user about I/O errors, or wrapping the entire input processor in a
`try/catch`, our program may choose to suppress exceptions, especially in case the I/O is non-critical.

```scala
// reading file into Option type using generators
// fail silently
def readFromFileIntoOption(filename: String): Option[List[String]] = {
  try {
    val buffer = Source.fromFile(filename)
    val lines = (
      for (line <- buffer.getLines)
        yield line
      ).toList

    buffer.close
    Some(lines)
  } catch {
    // any exception will results to None
    case e: Exception => None
  }
}
```

Using `for/yield` syntax, we easily convert a `BufferedSource` to a `List`. Types transformation is quite similar
to the above example.

Our `readFromFileIntoOption` has a deterministic output type: `Option`, or in other words,
we know it will always return an instance of `Option`.
By using it, we're not worried about it throwwing error or stopping our program execution flow,
instead we just simply use Scala pattern matching or `map` later on:

```scala
val lines = readFromFileIntoOption("input.txt")
lines.map(_.foreach(println))
```

or in a more imperative style:

```scala
val optionLines = readFromFileIntoOption("input.txt")
optionLines match {
  case Some(lines) => lines.foreach(println)
  case None =>
}
```

### Write to a file

Similar pattern of with / without `Option` for writing to files, however both approaches serve the same purpose.
Unlike read, which is usually at the beginning of some logic and having the input type determined gains us benefits,
write is usually a void function with no return types, and called at the end of execution (result, log, etc.).

```scala
// write to file
// stdout exception when fail
def writeToFile(filename: String, contents: String) {
  try {
    val writer = new PrintWriter(new File(filename))
    writer.write(contents)
    writer.close
  } catch {
    case e: FileNotFoundException => println(s"Cannot write into file ${filename}.")
    case e: Throwable => println(s"Error ${e.getMessage} when writing to file ${filename}.")
  }
}

// using Option to wrap writing to file
// with this method, if we can't write to file, nothing will be executed
def optionWriteToFile(filename: String, contents: String) {
  val writer: Option[PrintWriter] =
  try {
    Some(new PrintWriter(new File(filename)))
  } catch {
    case e: Exception => None
  }
  writer.foreach { w => w.write(contents); w.close }
}
```

In both examples, we use Java's provided `PrintWriter` with `try / catch` block to instantiate a writer instance.

Usages are straightforward, simply call the function:

```scala
writeToFile("output.txt", "I am a string.\n")
optionWriteToFile("output2.txt", "There another string.\n")
```

The only noticeable difference with the second example is that if we modify the function to returns an
`Option[PrintWriter]` instance, we allow the caller re-use it multiple times writing non-critical outputs to files
(e.g. aggregating logs):

```scala
def optionWriteToFile(filename: String): Option[PrintWriter] = try {
  Some(new PrintWriter(new FileWriter(filename, true)))
} catch {
  case e: Exception => None
}
```

Slightly modified usage:

```scala
val aggregateWriter = optionWriteToFile("output.txt")
aggregateWriter.foreach { w => w.println("appending to file"); w.close }
```
