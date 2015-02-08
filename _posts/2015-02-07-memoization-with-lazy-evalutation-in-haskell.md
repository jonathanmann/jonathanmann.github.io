---
layout: post
title: Stepping Through Memoization in Haskell
---

To better understand how memoization works with Haskell's lazy evaluation, let's walk through a simple example step by step. As a learning tool, we'll examine a simple function that raises the number two to a the power of whatever number is given as input. Let's begin by improving the [naive implemenation of the function](https://github.com/jonathanmann/blog_examples/blob/master/recursion_in_haskell/r_two_to_power.hs) that we explored in the [previous post](http://jonathanmann.github.io/2015/02/03/recursion-in-haskell/).

### Naive Implementation

Consider the [naive implementation](https://github.com/jonathanmann/blog_examples/blob/master/recursion_in_haskell/r_two_to_power.hs) :

{% highlight hs %}
r_two_to_power :: Int -> Integer
r_two_to_power 0 = 1
r_two_to_power n = r_two_to_power(n-1) + r_two_to_power(n-1)
{% endhighlight %}

This implementation returns the correct result, but it could be improved to become much faster with memoization.

### Visualization
To understand why the naive implementation is so inefficient consider the following diagram :
![recursion_tree](http://jonathanmann.github.io/public/img/recursion_tree.png)

For every node in the tree, all child nodes must be evaluated in order to return their results to the parent node. Unfortunately, this ends up causing the same problem to be evaluated over and over again across multiple levels. For efficiency, what we would really like to produce is a process that looks more like the following :

![m_recursion_tree](http://jonathanmann.github.io/public/img/m_recursion_tree.png)

In our new model, the number of calculations for each additional step expands linearly as opposed to exponentially, but, in order to accieve this end, we will need to create a memoized implementation of the function.

### Memoized Implementation

The [memoized implementation](https://github.com/jonathanmann/blog_examples/blob/master/memoization_in_haskell/m_two_to_power.hs) will look very similar to the naive implementation, but with a few key distinctions. We'll walk throught the differences line by line.

{% highlight hs %}
m_two_to_power :: Int -> Integer
m_two_to_power = (map two_to_power [0 ..] !!)
    where two_to_power 0 = 1
          two_to_power n = m_two_to_power(n-1) + m_two_to_power(n-1)
{% endhighlight %}


### Explanation

Let's start from the beginning.
{% highlight hs %}m_two_to_power :: Int -> Integer{% endhighlight %}
For the first line, the only difference from the naive implementation is that we've switched the leading letter from 'r' to 'm' to indicate that this is a memoized version of the function.
The second line is where things start to get interesting:
{% highlight hs %}m_two_to_power = (map two_to_power [0 ..] !!){% endhighlight %}
Here we define all cases of m_two_to_power as mapping to the corresponding output of the function two_to_power given the same input. 

In haskell, "[0 ..]" means a list that begins at zero and continues on forever. This type of operation is only possible because of Haskell's lazy evaluation. Because nothing from the list has been called, the list does not currently need to be evaluated so the operation is valid. The double exclamation points tell Haskell to index the list.

But wait! The function "two_to_power" has not been defined! Won't this break the function? I'm glad you've asked. To understand what's going on, let's look at the next line.
{% highlight hs %}
    where two_to_power 0 = 1
{% endhighlight %}
In Haskell, you can define sub-functions after the where clause which can be called within the main fuction body. Here a base case is defined for the sub-function "two_to_power".
{% highlight hs %}
          two_to_power n = m_two_to_power(n-1) + m_two_to_power(n-1)
{% endhighlight %}
In the final line, the general case for "two_to_power" is defined recursively in terms of its parent function. In order to understand, how this works, let's walk step by step through an example.

### Example

Let's step through the function when we input the value of 3. 
{% highlight hs %}
m_two_to_power 3
{% endhighlight %}

First the function, m_two_to_power, looks to the mapped sub-function, two_to_power, for a value.



### Step Table

<table>
  <thead>
    <tr>
      <th>Step</th>
      <th>Value</th>
    </tr>
  </thead>
  <tfoot>
    <tr>

      <td>1</td>
      <td>23</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>

      <td>2</td>
      <td>11</td>
    </tr>
    <tr>

      <td>3</td>
      <td>3</td>
    </tr>
    <tr>

      <td>4</td>
      <td>9</td>
    </tr>
  </tbody>
</table>


