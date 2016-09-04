---
title: "Individual things"
teaching: 5
exercises: 5
questions:
- "What are some things in Python?"
objectives:
- "Assign variables in Python"
keypoints:
- "Variables are labels attached to values that are stored in the computer memory"
---

The most basic component of any programming language are "things", also called
variables or (in special cases) objects.

The most common basic "things" in Python are integers, floats, strings,
booleans, and some special objects of various types. We'll meet many of these as
we go through the lesson.

Here's a thing:

~~~
2
~~~
{: .python}

It's an integer, with the value 2. You can use the `print` function to show
multiple things in one cell:

~~~
print(2)
print("hello")
~~~
{: .python}

That second thing is a **string** (of characters). Things can be stored in
variables:

~~~
a = 1
b = "hello"
c = True
print(a, b, c)
~~~
{: .python}

We can use the `type` function to determine what kind of thing a variable is:

~~~
print(type(a))
print(type(b))
print(type(c))
~~~
{: .python}

### Commands that operate on things

While variable by themselves are pretty great, they are much more useful to us
when we can operate on them.

Standard math operators work as expected on numbers:

~~~
a = 2
b = 3
print(a + b)
print(a * b)
print(a ** b)  # You don't want ^
~~~

There are also operators for strings:

~~~
s1 = "hello"
s2 = "Neurohackweek"
print(s1 + s2)
print(s1 * 3)
print(s2 / 3)  
~~~
{: .python}

But not all math operators work on strings. For example, that last line raises
a nasty error:

~~~
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-14-9de011ead4c1> in <module>()
----> 1 print(s2 / 3)

TypeError: unsupported operand type(s) for /: 'str' and 'int'
~~~
{: .output}

This error tells us that the division operator (`/`) doesn't work for the
combination of a string (our variable `s2`) and an integer (the number 3).


> ### Integer and float division
>
> Division with integers would generate what some might consider surprising
> results on Python 2. For example, these two:
>
>    print(2 / 3)
>    print(2 / 3.0)   
>
> will give you different results if you are using Python 2. That's because
> Python distinguishes between integers (3) and floating point numbers and
> in Python 2 it would avoid up-casting integers to floats as much as possible.
> So, it would give you the integer division of integers (which in this case,
> evaluates to 0). Since this was somewhat surprising for many (and a cause of
> many bugs...), this was changed in Python 3.
{: .callout}

For exponentiation, use `**`, not `^` (it is an operator in Python, but it is the [bitwise xor operator](http://stackoverflow.com/a/2451393/3532933)):
~~~
print(2 ** 3)
print(2 ^ 3)
~~~
{: .python}

### Boolean operators compare two things

Boolean operators take one of two values: `True` or `False`, which are
constants of the language:

~~~
a = (1 > 3)
b = (3 == 3)
print(a)
print(b)
print(a or b)
print(a and b)
~~~
{: .python}

### Using functions to operate on variables

These will be very familiar to anyone who has programmed in any language, and
work like you would expect. There are many functions built into the language:

~~~
print(type(3))
print(len('hello'))
print(round(3.3))
~~~
{: .python}


> ### Getting help
>
> To find out what a function does, you can type it's name and then a
> question mark to get a pop up help window. Or, to see what arguments it takes,
> you can type its name, an open parenthesis, and hit tab. For example:
>
>     type?
> or:
>
>     type(<tab>
>
> This is an IPython/Jupyter feature and will not work in a regular
> Python session.
>
{: .callout}


### Many useful functions are in other libraries/packages

For example, let's meet `numpy`:

~~~
import numpy
type(numpy)
~~~
{: .python}

Alternatively, we can write:

~~~
import numpy as np
print(numpy == np)
~~~
{: .python}

This is shorter, and is also a very common convention

To see what is in a package or library, you can tab complete after typing a
`.`:

~~~
np.<tab>
~~~
{: .python}

Here are some example of numpy functions and numpy things:

~~~
print(np.sqrt(4))  # A function
print(np.pi)  # A function
print(np.sin(np.pi)) # A function called on a thing
~~~
{: .python}

### Objects and methods

Before we get any farther into the Python language, we have to say a word about
"objects". We will not be teaching object oriented programming in this tutorial,
but you will encounter objects throughout Python.

In the simplest terms, you can think of an object as a small bundled "thing"
that contains within itself both data and functions that operate on that data.
For example, strings in Python are objects that contain a set of characters and
also various functions that operate on the set of characters. When bundled in an
object, these functions are called "methods". Instead of the "normal"
`function(arguments)` syntax, methods are called using the syntax
`variable.method(arguments)`

A string is an object of the class `string`:

~~~
a = 'um, hullo?'
print(type(a))
~~~
{: .python}

Objects of this class have some methods bundled in them. For example:

~~~
print(a.capitalize())
print(a.replace('l', 'X'))
~~~
{: .python}

To see the methods of an object, tab-complete on the object:

~~~
a.<tab>
~~~
{: .python}


> ### EXERCISE 1 - Introducing logistic growth
>
> Throughout this lesson, we will successively build towards a program that
> will calculate the logistic growth of a population of bacteria in a petri
> dish (or bears in the woods, if you prefer).
>
> As a reminder, a commonly used discrete time equation for logistic population
> growth is
>
> $n[t+1] = n[t] + r \cdot n[t] \cdot (1 - \frac{n[t]}{K})$
>
> where n(t) is the population size at time t, r is the net per capita growth
> rate, and K is the carrying capacity of the dish/woods.
>
> To get started, write Python expressions that do the following:
> 1. Create variables for `r`, `K`, and `n0`, setting these equal to 0.6, 100,
>     and 10, respectively.
> 1. Create the variable `n1` and calculate it's value. Do the same for `n2`.
> 1. Check the type of `n2` - what is it?
> 1. Modify your calculations for `n1` and `n2` so that these values are
>    rounded to the nearest integer.
>
> __Bonus__
>
> 1. Test whether `n2` is larger than 20, and print out "n2 more than 20: "
>    followed by the answer (either True or False).
> 1. Figure out how to test whether `n2` is an integer (a mathematical integer,
> not necessarily whether it is an integer type) (HINT: look at the methods of
> `n2` by typing `n2.` and pressing tab.)
