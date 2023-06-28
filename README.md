# Table of Contents
- [Main](README.md)

[Basics](#basics)
1. [variables](#variables)
1. [data types](#data-types)
1. [data structures](#data-structures)
1. [operators](#operators)
1. [functions](#functions)
1. [packages](#packages)
1. [control](#control)

[OOP](#OOP)

# Basics

### variables

```scala
var x = 5 // variable
var x: Double = 5 // explicit type variable

val y = 5 // constant
```

### data types
```scala
val x: Unit = () // singleton (like void)
val x: Boolean = true
val x: Byte = 10
val x: Short = 1000
val x: Int = 42
val x: Long = 1234567890L
val x: Float = 3.14f
val x: Double = 3.14159
val x: Char = 'A'

x.isInstanceOf[String] // check type
x.asInstanceOf[String] // cast
```

### data strucutres
```scala
val x: String = "Hello, World!"

val x: Array[Int] = Array(1, 2, 3, 4, 5)

val x: (Int, String) = (42, "Hello") // tuple
val (y,z) = x // deconstructing tuple

val x: Option[String] = Some("Hello")

val x: List[Int] = List(1, 2, 3, 4, 5) // list (immutable)
1 :: List(2, 3) // cons

val x: Map[String, Int] = Map("one" -> 1, "two" -> 2, "three" -> 3)

// ranges
1 to 5 // include 5
1 until 6 // dont include 6
1 to 10 by 2
```

## operators
Arithmetic
- Addition: +
- Subtraction: -
- Multiplication: *
- Division: /
- Modulus (Remainder): %
- Comparison Operators:

Comparison
- Equality: ==
- Inequality: !=
- Greater than: >
- Less than: <
- Greater than or equal to: >=
- Less than or equal to: <=
- Logical Operators:

Logical
- Logical AND: &&
- Logical OR: ||
- Logical NOT: !
- Bitwise Operators:

Bitwise
- Bitwise AND: &
- Bitwise OR: |
- Bitwise XOR: ^
- Bitwise NOT: ~
- Left Shift: <<
- Right Shift: >>
- Unsigned Right Shift: >>>
- Assignment Operators:

Assignment
- Simple assignment: =
- Addition assignment: +=
- Subtraction assignment: -=
- Multiplication assignment: *=
- Division assignment: /=
- Modulus assignment: %=
- Bitwise AND assignment: &=
- Bitwise OR assignment: |=
- Bitwise XOR assignment: ^=
- Left shift assignment: <<=
- Right shift assignment: >>=
- Unsigned right shift assignment: >>>=

### functions

```scala
// define function
def f(x: Int) = {
    x*x // returns last statement
}

def f(x: Any) // call-by-value
def f(x: => Any) // call-by-name (lazy parameters)

// anonymous functions
(x: Any) => x*x
x => x*x
// underscore is positionally matched arg when calling anonymous function
(1 to 5).map(_ * 2) 
(1 to 5).reduceLeft(_+_)
// block stype anonymous function in use
(1 to 5).map { x =>
  val y = x * 2
  println(y)
  y
}
// pipeline style of anonymous functions in use
(1 to 5) filter {
  _ % 2 == 0
} map {
  _ * 2
}

// currying
def zscore(mean: R, sd: R) =
  (x: R) =>
    (x - mean) / sd
// is the same as 
def zscore(mean: R, sd: R)(x: R) =
  (x - mean) / sd
val normer = zscore(7, 0.4) _ // in use

// generic types
def mapmake[T](g: T => T)(seq: List[T]) =
  seq.map(g)

// variable number of arguments
def sum(args: Int*) =
  args.reduceLeft(_+_)
```

### packages

``` scala
// declare a package
package pkg // at start of file

// Packaging by scope
package pkg {
  ...
}

// Package singleton (can only make one instance at a time)
package object pkg {
  ...
}

// import packages
import scala.collection._ // wildcard import
import scala.collection.Vector // selective import
import scala.collection.{Vector, Sequence} // selective imports
import scala.collection.{Vector => Vec28} // rename import
import java.util.{Date => _, _} // import all except Date
```

### control
```scala
// if
if (x) print("hi") else print("bye")
if (x) print("hi")

// while
while (x < 5) {
    println(x)
    x += 1
}

// for
for (x <- xs) {
    println(x)
}
// for-comprehension (same as filter,map)
for (x <- xs if x % 2 == 0)
    yield x * 10

// matching
(xs zip ys) map {
    case (x, y) => x * y
}
// match to current val (use backticks, unless uppercased V42, i know it's weird)
val v42 = 42
3 match {
  case `v42` => println("42")
  case _     => println("Not 42")
}
```

# OOP
``` scala
// class
class C(x: Int)
var c = new C(4)

class C(val x: Int) // automatic public member defined
var c = new C(4)
c.x

class C(var x: R) { // constructor is class body
  assert(x > 0, "positive please") // check input
  var y = x // declare public member
  val t = 5 // gettable but not settable
  private var z = 1 // declare a private member
  def this() = this(42) // alternative constructor
}

// anonymous class
new {
  ...
}

// abstract class (non-createable)
abstract class D { ... }

// inherit
class C extends D { ... }
class D(var x: R)
class C(x: R) extends D(x)

// singleton (can only make one instance at a time)
object O extends D {...}

// trait (like interface)
trait T { ... }
class C extends T { ... }
class C extends D with T { ... }

// method overrides in class
class C extends D { override def f = ...}
```
