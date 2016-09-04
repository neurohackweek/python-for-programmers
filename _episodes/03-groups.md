---
title: "Collections: groups of things"
teaching: 5
exercises: 5
questions:
- "What are collections of things?"

objectives:
- "Assign collections in Python"
- "Understand the differences and similarities between lists, dicts, tuples and arrays"

keypoints:
- "Python contains several built-in collection types"
- "Numpy extends these with an array type"
- ""
---


Once the number of variables that you are interested in starts getting large,
working with them all individually starts to get unwieldy. To help stay
organized, we can use collections of things.

Probably 99% of your work in scientific Python will use one of four types of
collections: lists, tuples, dictionaries, and numpy arrays. We'll look quickly
at each of these and what they can do for you.

### Lists

Lists are probably the handiest and most flexible type of container. Lists are
declared with square brackets []. Individual elements of a list can be selected
using the syntax `a[ind]`.

Lists are created with square bracket syntax:

~~~
a = ['hi', 'hello', 'yo']
print(a, type(a))
~~~
{: .python}

Lists (and all collections) are also indexed with square brackets:

~~~
print(a[0])
print(a[1])
~~~
{: .python}

**NOTE: The first item has index zero, not one!**

Lists can be sliced by putting a colon between indexes

~~~
print(a[0:2])
~~~
{: .python}

**NOTE: Indexing is 0-based, and the end value is not inclusive**

You can leave off the start or end if desired:

~~~
print(a[:2])
print(a[2:])
print(a[:-1])
~~~
{: .python}


Lists are objects, like everything else, and have methods such as append:

~~~
a.append('hiya')
print(a)

a.append([1,2])
print(a)

print(a.pop())
print(a)
~~~
{: .python}

**Note: Lists can have mixed types**

__TIP:__ A 'gotcha' for some new Python users is that many collections,
including lists, actually store pointers to data, not the data itself. This
makes the language much more efficient, but can lead to some very hard to trace
bugs...


Assigning b = a does not make a copy of a, rather b and a now point to the same
data

~~~
b = a
print(a, b)
b[0] = 'bye'
print(a, b)
b[0] = 'hi'
~~~
{: .python}

To instead make a copy, use either list(a) or a[:]

~~~
b = list(a)
print(a, b)
b[0] = 'seeya'
print(a, b)
~~~
{: .python}

> # Storing population size in a list
>
> Using your previous code for logistic growth do the following:
> 1. Modify your code so that the values of `n0`, `n1`, `n2`, and `n3` are stored in a list and not as separate individual variables. HINT: You can start off by declaring an empty list using the syntax `n = []`, and then append each new calculated value of `nt` to the list.
>  2. Get the first and last values in the list, calculate their ratio, and print out "Grew by a factor of " followed by the result.
> __Bonus__

> 1. Extract the last value in two different ways: first, by using the index for the last item in the list, and second, presuming that you do not know how long the list is.
> 2. Change the values of `r` and `K` to make sure that your cell still runs correctly and gives reasonable answers.
{: .challenge}


>
>     r = 0.6
>     K = 100
>     n = []
>     n.append(10)  # Append n0 in the first location
>     n.append(round(n[0] + r*n[0] * (1 - n[0]/K)))  # Append n1
>     n.append(round(n[1] + r*n[1] * (1 - n[1]/K)))  # Append n2
>     n.append(round(n[2] + r*n[2] * (1 - n[2]/K)))  # Append n3
>     print(n)
>
>     print("Grew by a factor of ", n[3]/n[0]) # or n[-1]/n[0]
{: .solution}


### Tuples

We won't say a whole lot about tuples except to mention that they basically work
just like lists, with two major exceptions:

1. You declare tuples using () instead of []
2. Once you make a tuple, you can't change what's in it

You'll see tuples come up throughout the Python language, and over time you'll
develop a feel for when to use them. In general, they're often used instead of
lists to group items when the position in the collection is critical to
understanding the item's meaning, such as `(x,y)`, and when you want to make
sure that you don't accidentally modify any of the items later.

~~~
a = (1,2)
print(a[-1])
~~~
{: .python}

Once allocated, tuples are *immutable*. For example, try:

~~~
a[0] = 1
~~~
{: .python}


### Dictionaries

Dictionaries are the collection to use when you want to store and retrieve
things by their names (or some other kind of key) instead of by their position
in the collection. A good example is a set of model parameters, each of which
has a name and a value. Dictionaries are declared using {}.

~~~
params = {'n0': 10, 'r': 0.5}
print(params)
print(params['r'])
~~~
{: .python}

Once created, it can be extended:

~~~
params['K'] = 200
print(params)
~~~
{: .python}

### Numpy arrays (`ndarrays`)

Even though numpy arrays (or `ndarrays`, for n-dimensional arrays) are not part
of the core Python libraries, but they are so useful in scientific Python that
we're including them here in this introduction lesson. Numpy arrays are
collections of things, all of which must be the same type, that work similarly
to lists (as we've described them so far). The most important are:

1. You can easily perform elementwise operations (and matrix algebra) on arrays
2. Arrays can be n-dimensional
3. Arrays must be pre-allocated (ie, there is no equivalent to append)

Arrays can be created from existing collections such as lists, or instantiated
"from scratch" in a few useful ways.

When getting started with scientific Python, you will probably want to try to
use `ndarrays` whenever possible, saving the other types of collections for
those cases when you have a specific reason to use them.

You can make an array out of a list:

~~~
import numpy as np  # Just to be sure

alist = [2, 3, 4]
blist = [5, 6, 7]
a = np.array(alist)
b = np.array(blist)
print(a, type(a))
print(b, type(b), b.dtype)
~~~
{: .python}

You can do arithmetic on arrays:

~~~
print(a**2)
print(np.sin(a))
print(a * b)
print(a.dot(b), np.dot(a, b))
~~~
{: .python}


Boolean operators work on arrays too, and they return boolean arrays:

~~~
print(a > 2)
print(b == 6)

c = a > 2
print(c)
print(type(c))
print(c.dtype)
~~~
{: .python}



Indexing arrays is similar to list indexing, but if the array has more than one
dimension, we index separately on each dimension:

~~~
print(a[0:2])

c = np.random.rand(3,3)   # This is another way of making an array
print(c)
print(c[1:3,0:2])

c[0,:] = a
print(c)
~~~

Arrays can also be indexed with other boolean arrays:

~~~
print(a)
print(b)
print(a > 2)
print(a[a > 2])
print(b[a > 2])

b[a == 3] = 77
print(b)
~~~
{: .python}

`ndarrays` have *attributes* in addition to methods:

~~~
print(c.shape)
print(c.prod())
~~~
{: .python}


There are handy ways to make arrays full of ones and zeros:

~~~
print(np.zeros(5), '\n')
print(np.ones(5), '\n')
print(np.identity(5), '\n')
print(np.eye(5), '\n')
~~~
{: .python}


You can also easily make arrays of number sequences

~~~
print(np.arange(10))
print(np.arange(0, 10, 2))
print(np.linspace(5, 10, 33))
~~~
{: .python}
