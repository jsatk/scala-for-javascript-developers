# Scala for Javascript Developers

_By [Jesse Atkinson](https://jsatk.us), Software Engineer at [Credit Karma](https://www.creditkarma.com/).  Published on MM, DD, YYYY.  This article is licensed for use under the [MIT License](https://github.com/jsatk/scala-for-javascript-developers/blob/master/LICENSE)._

_This article was inspired by [Kotlin for Python Developers](https://kotlinlang.org/docs/tutorials/kotlin-for-py/introduction.html) written by [Aasmund Eldhuset](https://eldhuset.net) and [A Road to Common Lisp](http://stevelosh.com/blog/2018/08/a-road-to-common-lisp/) written by [Steve Losh](http://stevelosh.com)._

---

Scala is a daunting language.  Even more so if you've only worked with loosely-typed interpreted languages like Javascript.  If you're coming from Javascript Scala, particularly Scala written in the Functional Programming style, can look like a cat walked across the keyboard.  When I was learning I would joke with my peers who actually knew Scala about the obtuseness of all the keywords.  What the hell is a `final sealed abstract case case` anyway?

This guide is my attempt to make the transition into Scala easier for everyone, but particularly aimed at those who are coming from a heavy Javascript background.  Even if you haven't worked heavily with Javascript, if you've primarily written in other popular loosely-typed interpreted languages such as Python or Ruby I think the same principals will apply.

The goals of this guide are as follows:

1. To explain why you might even consider Scala.  I hope by the end of this you will have teh answers to the questions: Why yet another language?  Why not use Java?  Why would I pick Scala over Kotlin?  Why would I use Scala when Typescript + Node.js is a thing?
2. To teach the fundamentals of Scala though the lens of the functional programing paradigm.
3. To relate Javascript to Scala.  For example: "I know how to `reduce` an array in Javascript.  How do I do similar in Scala?"
4. To teach some history of the language.  Some parts of Scala might seem strange at first, but if you know the history it will (hopefully) seem less strange.

## Contents

* [History](#history)
* [Installing](#installing)
* [Hello World](#hello-world)

## History

TODO

## Installing

TODO

## Hello World

One of the most frustrating things for me coming from Javascript to Scala was my inability to just _do_ things.  I wanted to write some code and see it run.  Scala isn't really set up for this in the same way Javascript is, but I understand your enthusiasm to get something running.  So lets do that.

Fire up your favorite editor and create a file called `helloWorld.scala`.  Input the following:

```scala
object HelloWorld {
  def main(args: Array[String]): Unit = {
    println("Hello, world!")
  }
}
```

Okay.  Now lets run it!  (This assumes that both the Scala software and the user environment are set up correctly.  If it isn't please jump over to the [installing](#installing) section.)

```sh
$ scala helloWorld.scala
Hello, world!
```

If all has gone well so far... Congratulations!  You've written your first Scala program and successfully ran it.

Lets take a minute and talk about these five lines of code.

The `def` keyword is to Scala what the `function` keyword is to Javascript.  Scala also has lambda functions AKA arrow fucntions much like Javascript, but we're not going to get into that at the moment.

If you've worked with Java before seeing the `main` function should be similar to you.  It's the entry point of the program.

Also note we've wrapped this function in an `object`.  This is required.  We can't define functions at the top level, so we must give it a "namespace".  Here our namespace is `HelloWorld`.

The function `main` has one parameter: `args`.  The `: Array[String]` bit after `args` is us telling the Scala compiler (and anyone reading the code) what `args` is.  In this case you would say that it is "an array of strings".  Next there is `: Unit`.  `Unit` is to Scala what `undefined` is to Javascript.  In fact, here we could leave it off.  The compiler is smart enough to infer that this `main` function returns nothing AKA `Unit`.  As I said earlier though, writing code is both for the compiler and for the reader.  Seeing `Unit` here lets any readers know that this function doesn't return anything and is most-likely a side-effect function (TODO: Jesse clean up this sentence).

Next there's the method `println`.  This is a globally available method.  You would also say it is an _implicit_ method.  `println` accepts anything as an argument and attempts to print it out.  It also returns nothing AKA `Unit`.

Lastly, you'll notice the `=` as well as the `{}`.  We assign the block of code contained in the curly braces via the `=` symbol to the function name `main`.  If your method is only one-line long you don't need the curly braces.

In most Scala programs you need to first compile the `.scala` file which will produce compiled byte code that the computer can read.  However for simple programs such as our above "Hello World" script the Scala compiler can actually run it without having to compile it.

An alternative (and more common) way to run this program would be to run the following:

```sh
$ scalac helloWorld.scala
$ scala HelloWorld
Hello, World!
```

If you were to run the shell command `ls` in the directory where you created `helloWorld.scala` you'd now see two more files in there: `HelloWorld$.class` & `HelloWorld.class`.  This is what allows us to run `$ scala HelloWorld` in the above command.

Now that you've written a basic program in Scala lets go over some other brief basics.

Comments in Scala are the same as in Javascript.  `//` for one-line-ers and `/* */` for mutli-line-ers.  You may be familiar with JS Docs or Javadocs.  Scala has... you guessed it... Scaladocs.  Confusingly the convention for Scaladoc allows for the `*` to align on column two _or_ three.  All it cares about is that you're consistent.  In most projects I've seen these days the consensus seems to be aligning on column two.

For example:

```scala
/**
 * This function does something very awesome.
 */
```

Or – again – you can align on column three.

```scala
/**
  * This function does something very awesome.
  */
```

Semicolons are still a thing in Scala, but the use of them is discouraged.  The following is all valid Scala and, again, doesn't require a semicolon.

```scala
1 + 2
val f = foo
          .bar()
          .baz()
val g = foo.
          bar().
          baz()
```

Notice the placement of the `.` in the method chain?  Scala doesn't care where you place it.  As of this writing there doesn't seem to be a consensus in the community as to which is "better".  I have my own preference which I will elect not to share, but the important thing is to be consistent in which ever you choose.

The last thing I'd like to cover in this "Hello World" section is `return` statements.  [Don't use them](https://blog.knoldus.com/scala-best-practices-say-no-to-return/).  They're unnecessary.  All Scala methods return the value of the last statement implicitly.  This is most similar to a language like Ruby.

Lets go into the Scala [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop) (Read. Evaluate. Print. Loop.) by running `sbt console`.  And then write the following:

```scala
scala> def f(n: Int): String =
     | if (n % 2 == 0) {
     |   "even"
     | } else {
     |   "odd"
     | }
f: (n: Int)String

scala> f(2)
res0: String = even

scala> f(3)
res1: String = odd
```

Notice a few things: 1) We didn't need the `return` statement for the strings we wanted to return and 2) we didn't even need the curly braces `{}` for the code block we assigned to function `f`.  The `if` block is considered a _single_ statement.

Lets quit the Scala REPL by running `:q`.  If this looks familiar to you it's because it's [how you quit Vim](https://stackoverflow.blog/2017/05/23/stack-overflow-helping-one-million-developers-exit-vim/) (this author's beloved editor-of-choice).
