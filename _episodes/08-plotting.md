---
title: "Plotting with Matplotlib"
teaching: 10
exercises: 5
questions:
- "How can we visualize data?"
objectives:
- "Create plots from data"
keypoints:
- "Matplotlib is a library for 2D publication-quality scientific visualization"
- "MPL makes easy plots easy, and harder visualization possible."
---

### What is matplotlib?

Matplotlib is the most popular and mature library for plotting data using
Python. It has all of the functionality you would expect, including the ability
to control the formatting of plots and figures at a very fine level.

The official matplotlib documentation is at [http://matplotlib.org/]([http://matplotlib.org/)
The matplotlib gallery is at [http://matplotlib.org/gallery.html](http://matplotlib.org/gallery.html)


### Importing matplotlib

Matplotlib is often used through 'pyplot', which provides a high-level interface
for plotting.

~~~
import matplotlib.pyplot as plt

# I almost always also import numpy at this point
import numpy as np
# The inline flag means that images will be shown here in the notebooks, rather
# than in pop-up windows.
%matplotlib inline
~~~


## 2. Creating Figures

There are two major challenges with creating figures. First is understanding the
syntax to actually make the basic plot appear. Second is formatting the basic
plot to look exactly how you would like it to look. In general, the formatting
will probably take you longer...

Within `pyplot` (currently imported as 'plt'), there are two basic ways to go
about making plots - using the Matlab-like clone (we saw that briefly before
with a call to `plt.plot`), and using the object-oriented approach. The latter
provides better control over plot features, while only requiring slightly more
typing. It's easy to quickly outgrow the Matlab clone, so we'll go right to the
object-oriented syntax.


### A first plot

In simple matplotlib plotting, there are two concepts to distinguish:

- __Figure__ - the entire figure, like what you might see in a journal, including all subplots, axes, lines, labels, etc. The whole encilada.  

- __Subplot/Axes__ - one of the sub-sections of the figure, labeled (a), (b), etc. in articles. Each subplot will contain one Axes object, which is the container where all of the useful stuff, such as actual lines, legends, labels, etc., are actually housed.

For example, here's how to make one figure with two subplots, the second of
which contains two lines.

~~~
# Make some data to plot
x = np.linspace(0, 2*np.pi)
y1 = np.sin(x)
y2 = np.cos(x)

# First, create an empty figure with 2 subplots
# - The arguments (1, 2) indicate 1 row and 2 cols
# - The function plt.subplots returns an object for the figure and for each axes
# - There are multiple ways to accomplish this same goal, but this is probably the
#   simplest - notice that each subplot is associated with one of the axes objects.
fig, (ax1, ax2) = plt.subplots(1, 2)

# Next, put one line on the first axis and both lines on the second axis
# - On the second axes, add a legend to distinguish the two lines
ax1.plot(x, y1)

ax2.plot(x, y1, label='sin')  # The labels are what appear in the legend
ax2.plot(x, y2, label='cos')
ax2.legend()

# Finally, save the figure as a png file
fig.savefig('myfig.png')
~~~
{: .python}


> ## Simple formatting
>
> There are lots of formatting options to play with. Modify the code above to
> make some changes to the formatting of these plots.
>
> First, make some changes to the axes. HINT: These adjustments are methods to  > the ax1 and ax2 objects, and (conveniently) they all start with the text
> 'set_'. Try typing 'ax1.set_' and hitting tab to see some options.
>
> * Change the x axis on ax1 to run from 0 to 4. (HINT: set_xlim)
> * Add labels to the x axis on both subplots (HINT: set_xlabel, set_ylabel)
>
> Second, make some changes to the lines that you plotted using ax1.plot(...).
> These changes can be made by looking at the various arguments that you can
> give to the plot method. You can do this easily by typing ax1.plot? in the
> cell below and running it - this will give you pop-up help for the plot
> method.
>
> * Make the sine line on ax1 red and dashed.
> * Put a circular black marker on top of the cos line on ax2. Make it really
> big.
>
> _Bonus_: Eliminate the box around the legend on the second subplot.


### Other types of plots

In the example above, we used the plot method to make line plots. There are also
methods to make scatter plots, barplots, histograms, loglog plots, semilog
plots, etc.

~~~
# Make some data to plot
x = np.arange(0, 100)
y = np.random.rand(100)  # 100 random numbers

# Make a figure with 6 subplots and axes
fig, ((ax1, ax2), (ax3, ax4), (ax5, ax6)) = plt.subplots(3, 2)

# Add data to each axis. Optional arguments to each method will customize each plot.
ax1.plot(x, y)
ax2.hist(y)
ax3.scatter(x, y)
ax4.boxplot(y)
ax5.loglog(x, y)
ax6.semilogx(x, y)
~~~

### Plotting images

Matplotlib also makes it easy to plot images. For this, you can use the plot
method imshow (syntax borrowed from Matlab).

For this, you can download some data from [here](https://github.com/neurohackweek/python-for-programmers/blob/gh-pages/data/brain.zip?raw=true). Unzip the folder in the directory in which you are currently working. Then:

~~~
# Read an image file for first subplot, generate random array for second
image_data = np.load('brain/slice1.npy')
# If you have images in a standard format (e.g. jpg), you can do this:
# img1 = plt.imread('image.jpg')
img2 = np.random.rand(128, 128)

# Make figure
fig, (ax1, ax2) = plt.subplots(1, 2)
ax1.imshow(img1)
ax2.imshow(img2)

ax1.set_axis_off()  # Hide "spines" on first axis
~~~
{: .python}


> Smoothing and `matshow`
>
> Note that `imshow` applies smoothing to the image. You can turn off this
> smoothing, using the `interpolation` key-word argument. Another option is
> to use the `matshow` function instead. That one does not apply smoothing.


## The matplotlib gallery

It can be very intimidating to try to craft exactly the figure that you want,
especially if you are used to being able to adjust things visually using a
program like Excel.

If you get stuck and don't know where to start, or just want to learn more about
what matplotlib can do, a great option is to have a look at the matplotlib
gallery, which can be found at
[http://matplotlib.org/gallery.html](http://matplotlib.org/gallery.html). A good
way to get started is to find a figure here that sort of looks like what you
want, copy the code, and modify it for your own needs.


> ### Exploring the matplotlib gallery
>
> Have a look at the matplotlib gallery, find a cool looking figure, copy the
> code a cell in your notebook and modify it. Note that some of the examples
> might require packages that are not installed on your machine (in particular
> those that make maps) - if this is the case, pick another example for the
> purposes of this exercise.
>
> In Jupyter, you can use the `%load`. Type `%loadpy` and then the URL of the
> py file containing the code, and it will automatically copy it into a cell
> below. Run the cell with the code to see the figure.
>
> Tweak the figure to your liking -- use your creativity!
