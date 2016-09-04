---
title: "Repeating operations"
teaching: 10
exercises: 5
questions:
- "How can we repeat operations?"
objectives:
- "Use for and while loops in a program"
keypoints:
- "Repeating operations over items of a collection makes sense"
- "Both for and while loops can be used to repeat operations in different cases"
---

So far, everything that we've done could, in principle, be done by hand
calculation. In this section and the next, we really start to take advantage of
the power of programming languages to do things for us automatically.

We start here with ways to repeat yourself. The two most common ways of doing
this are known as for loops and while loops. `for` loops in Python are useful
when you want to cycle over all of the items in a collection (such as all of the
elements of an array), and `while` loops are useful when you want to cycle for
an indefinite amount of time until some condition is met.

The basic examples below will work for looping over lists, tuples, and arrays.
Looping over dictionaries is a bit different, since there is a key and a value
for each item in a dictionary. Have a look at the Python docs for more
information.


A basic for loop:

~~~
wordlist = ['hi', 'hello', 'bye']
for word in wordlist:
    print(word + '!')
~~~

The indentation is crucial. The loop will operate over all the lines within the
indented block for each item in the collection, and then pop out.

Another example -- sum all of the values in a collection using a for loop:

~~~
numlist = [1, 4, 77, 3]

total = 0
for num in numlist:
    total = total + num

print("Sum is", total)
~~~

Often we want to loop over the indexes of a collection, not just the items

~~~
print(wordlist)

wordrange = np.arange(len(wordlist))
print(wordrange)

for i in wordrange:
    print(i, wordlist[i])
~~~
{: .python}

> ## `enumerate`
>
> The pattern above is so useful, that there's a key-word in the language
> for it:
>
>     for i, word in enumerate(wordlist):
>         print(i, word)
>
>
{: .callout}


While loops are useful when you don't know how many steps you will need, and want to stop once a certain condition is met:

~~~
step = 0
prod = 1
while prod < 100:
    step = step + 1
    prod = prod * 2
    print(step, prod)

print('Reached a product of', prod, 'at step number', step)

~~~
{: .python}


Once we start really generating useful and large collections of data, it becomes
unwieldy to inspect our results manually. The code below shows how to make a
very simple plot of an array. We'll do much more plotting later on, this is just
to get started. For this, we will use the `matplotlib` library (installed via:
`conda install matplotlib`):


~~~
import matplotlib.pyplot as plt
%matplotlib inline  ## This is an IPython command that makes sure plots are in the notebook

y = np.arange(100)**2
plt.plot(y)
~~~
{: .python}


> Using loops to repeat calculations
>
> FINALLY, let's get smart about our calculations of `nt`. Copy your code from
> Exercise 3, and adjust it to do the following:
> 1. Write a for loop to fill in the values of `nt` for 100 time steps. HINT: You will need to create an array of the step numbers using a command like `step = np.arange(1, 100)`. (Why does this array start at 1 and not at 0?). Then, loop over the values of the step array, and use each step value to index the array `n`.
> 2. Plot the array `n`.
> 3. Play around with the values of `r` and `K` and see how it changes the plot. What happens if you set `r` to 1.9 or 3?
>
> __Bonus__
>
> 1. Modify your code to use a while loop that will stop your calculation once the population size is greater than 90. HINT: Start a step counter `i` at 1, and check that the value in `n[i-1]` is less than 90 each time around the loop. Increment the step counter within the loop so that you have a record of what step the calculation stopped at.
{: .challenge}


>     r = 0.6
>     K = 100
>     n = np.zeros(100, dtype=float)
>     n[0] = 10
>
>     steps = np.arange(1, 100)
>     for i in steps:
>         n[i] = round(n[i-1] + r*n[i-1] * (1 - n[i-1]/K))
>
>     plt.plot(n)
{: .solution}

>     r = 0.6
>     K = 100
>     n = np.zeros(100)
>     n[0] = 10
>
>     i = 1
>     while n[i-1] < 90:
>         n[i] = round(n[i-1] + r*n[i-1] * (1 - n[i-1]/K))
>          print(i, n[i])
>        i = i + 1
>
> print('Ended with a population size of', n[i-1], 'at step', i-1)
> print('Population sizes to this step were', n[0:i])
{: .solution}
