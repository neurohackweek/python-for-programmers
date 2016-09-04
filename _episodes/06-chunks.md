---
title: "Creating reusable chunks with functions"
teaching: 5
exercises: 5
questions:
- "How can we avoid repeating ourselves?"
objectives:
- "Define a function to perform a computation and reuse it"
- "Create a module that can be imported into data analysis notebooks"
keypoints:
- "Writing functions allows us to modularize our code and reuse it"
- "DRY -- Don't repeat yourself"
---

One way to write a program is to simply string together commands, like the ones
described above, in a long file, and then to run that file to generate your
results. This may work, but it can be cognitively difficult to follow the logic
of programs written in this style. Also, it does not allow you to reuse your
code easily - for example, what if we wanted to run our logistic growth model
for several different choices of initial parameters?

The most important ways to "chunk" code into more manageable pieces is to create
functions and then to gather these functions into modules, and eventually
packages. Below we will discuss how to create functions and modules. A third
common type of "chunk" in Python is classes, but we will not be covering
object-oriented programming in this workshop.

We've been using functions all day:

~~~
x = 3.333333
print(round(x, 2))
print(np.sin(x))
~~~
{: .python}

It's easy to write your own functions

~~~
def multiply(x, y):
    """
    Multiply two numbers

    Parameters
    ----------
    x, y : integer float

    Returns
    -------
    mul : float/integer
        The product of the inputs
    """
    return x*y
~~~
{: .python}

Once a function definition is "run" and saved in memory, it's available just
like any other function

~~~
print(type(multiply))
print(multiply(4, 3))
~~~
{: .python}


All arguments must be present, or the function will return an error:

~~~
mutliply(4)
~~~
{: .python}

Keyword arguments can be used to make some arguments optional by giving them a
default value. All mandatory arguments must come first, in order:

~~~
def multiply(x, y=10, to_print=False):
    """
    Multiply two numbers

    Parameters
    ----------
    x : integer or float
    y : integer or float (optional)
       Default : 10

    to_print : bool
        Whether to print the result

    Returns
    -------
    mul : float/integer
        The product of the inputs
    """
    mul = x * y
    if to_print:
        print(mul)

    return x*y
~~~
{: .python}


> Creating a logistic growth function

> Let's turn our logistic growth model into a function that we can use over and
> over again. Using your previous code do the following:
>
> 1. Turn your code into a function called `logistic_growth` that takes four arguments: `r`, `K`, `n0`, and `p` (the probability of a catastrophe). Make `p` a keyword argument with a default value of 0.1. Have your function return the `n` array.
> 2. Write a nice docstring describing what your function does.
> 3. In a subsequent cell, call your function with different values of the parameters to make sure it works. Store the returned value of `n` and make a plot from it.


> def logistic_growth(r, K, n0, p=0.1):
>     '''
>     Function to simulate discrete time stochastic logistic growth
>
>     Arguments
>     ---------
>     r : float
>         Reproductive rate of population
>     K : float
>         Carrying capacity
>     n0 : float
>         Initial population
>     p : float
>         Probability of a catastrophe resetting the population to n0
>
>     Returns
>     -------
>     n : ndarray
>         Array of 100 time steps of population values
>     '''
>
>     # Set up population array
>     n = np.zeros(100, dtype=float)
>     n[0] = n0

>     # Loop through all time steps
>     steps = np.arange(1, 100)
>     for i in steps:
>         cat = (np.random.rand() < p)  # Random catastrophe 10% of time
>         if cat:
>             n[i] = 10
>         else:
>             n[i] = grow_one_step(n[i-1], r, K)
>
>     return n
>
> def grow_one_step(nold, r, K):
>     """Calculate new population from old one."""
>     return round(nold + r*nold*(1 - nold/K))


~~~
a1 = logistic_growth(0.6, 100, 10)
a2 = logistic_growth(0.6, 100, 10)
a3 = logistic_growth(0.6, 100, 10)

plt.plot(a1)
plt.plot(a2)
plt.plot(a3)
~~~
{: .python}


### Putting the growth function(s) in a module

We can make our functions more easily reusable by placing them into modules that
we can import, just like we have been doing with `numpy`. It's pretty simple to
do this:

1. Copy your function(s) from Exercise 6 into a new text file, in the same directory as this notebook, called `pop.py`.
2. In the cell below, type `import pop` to import the module. Type `pop.` and hit tab to see the available functions in the module. Try running the logistic growth function that was imported from the module with a few different parameter values.

Congratulations! You've made a module that you can reuse in many different projects.
