---
title: "Making choices"
teaching: 10
exercises: 5
questions:
- "How can we select operations to execute, depending on the situation?"
objectives:
- "Use if statements and if-else clauses"
keypoints:
- "Logical operations can be instantiated using selection"
- "Flexible data analysis grows out of thats"
---

## Making choices

Often we want to check if a condition is True and take one action if it is, and
another action if the condition is False. We can achieve this in Python with an
if statement.

You can use any expression that returns a boolean value (True or False) in an
`if` statement. Common boolean operators are ==, !=, <, <=, >, >=. You can also
use `is` and `is not` if you want to check if two variables are identical in the
sense that they are stored in the same location in memory.

A simple if statement

~~~
x = 3
if x > 0:
    print('x is positive')
elif x < 0:
    print('x is negative')
else:
    print('x is zero')
~~~
{: .python}


If statements can rely on boolean variables

~~~
x = -1
test = (x > 0)
if test:
    print('Test was true')
~~~
{: .python}

> ### Making the model stochastic with an if statement
>
> Deterministic models are boring, so let's introduce some element of randomness
> into our logistic growth model. We'll model a simple "catastrophe" process, in
> which a catastrophe happens in 10% of the time steps that reduces the
> population back down to the size at n0. Building on your code from the
> previous exercise, do the following:
>
> 1. Inside your for loop, add a variable called `cata`, for catastrophe, that  will be True if a catastrophe has occurred, and False if it hasn't. A simple way to do this is to generate a random number using `np.random.rand()`, which will give you a pseudorandom number between 0 and 1. Check whether this number is less than 0.1 - this check will be True 10% of the time.
> 1. Using your boolean variable `cat`, add an if statement to your for loop that checks whether `cat` is true in each time step. If it is true, set the population back to the size at n[0]. Otherwise, perform the usual logistic growth calculation.
{: .challenge}

>
>     # Set up initial model parameters
> r = 0.6
> K = 100
> n = np.zeros(100)
> n[0] = 10

> # Loop through all time steps
> steps = np.arange(1, 100)
> for i in steps:
>     cat = (np.random.rand() < 0.1)  # Random catastrophe 10% of time
>     if cat:
>         n[i] = n[0]
>     else:
>         n[i] = round(n[i-1] + r*n[i-1] * (1 - n[i-1]/K))
>
> plt.plot(n)
>
> print('Population was above 50 in', np.sum(n > 50), 'out of 100 steps')
