# Working with matplotlib

Matplotlib is a Python library used for creating graphics. The library is large, but in this section we will review the basics. By the end of this section you will be able to: //idek
For this section, you will need to know basic **NumPy** and **pandas**. If you don't have experience with NumPy you can go to the NumPy section of this workshop.

## Pyplot

From matplotlib, we can import pyplot. Pyplot is used to either create a new Figure or Axes, or it can perform functions on existing ones. You can only manipulate one Figure or Axes at a time, and pyplot keeps track of the current one for you.

Matplotlib has on object oriented approach. If you are unfamiliar with **object oriented programming** (OOP), we had a [section of our Python workshop](https://github.com/HackBinghamton/PythonWorkshop/blob/master/Intermediate/BasicOOP.ipynb) you can check out for more info! Pyplot consists of [wrapper functions](https://megabyterose.com/2016/12/wrapper-functions/), which are used to handle the OOP for the most part. [Real Python](https://realpython.com/python-matplotlib-guide/#pylab-what-is-it-and-should-i-use-it) gives the following example,

> Calling  `plt.title()`  gets translated into this one line:  `gca().set_title(s, *args, **kwargs)`. Here’s what that is doing:
> -   `gca()`  grabs the current axis and returns it.
> -   `set_title()`  is a setter method that sets the title for that Axes object. The “convenience” here is that we didn’t need to specify any Axes object explicitly with  `plt.title()`.

You will see examples of objects in the **Object Hierarchy** section below.

## Object Hierarchy

A matplotlib plot contains a series of matplotlib objects. This is shown below.

![Chart](https://files.realpython.com/media/fig_map.bc8c7cabd823.png)

The outermost container is the Figure. The Axes are the second outermost container. Axes in maplotlib are not what we would assume. An Axes is an individual plot or graph, so a figure could contain multiple axes. The hierarchy continues with smaller objects, such as individual lines, text boxes and legends. Below is another image showing more of the smaller matplotlib objects.

![Chart: anatomy of a figure](https://files.realpython.com/media/anatomy.7d033ebbfbc8.png)


## Subplots

Now we will finally apply what we've been learning! Yay! We can call subplots function using pyplot. This is how we create make a Figure containing one Axes.

//code that shit

Once a plot is created, we can call methods on it to customize it. The following example is from [Real Python](https://realpython.com/python-matplotlib-guide/#pylab-what-is-it-and-should-i-use-it),

//COOODDEEE

Now let's check out another example, which creates two Axes on one Figure, from Real Python.

//coooooooooode

//not done :(

## Using Pandas

The pandas library contains some wrapper functions that make matplotlib calls. For example, the pandas `plot()` method is a wrapper for `plt.plot()`.

## Resources

 - [https://realpython.com/python-matplotlib-guide/#pylab-what-is-it-and-should-i-use-it](https://realpython.com/python-matplotlib-guide/#pylab-what-is-it-and-should-i-use-it)
