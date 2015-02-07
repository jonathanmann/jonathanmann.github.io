---
layout: post
title: Stepping Through Memoization in Haskell
---

To better understand how memoization works with Haskell's lazy evaluation, let's walk through a simple example step by step. As a learning tool, we'll examine a simple function that raises the number two to a the power of whatever number is given as input. Let's begin by improving the [naive implemenation of the function](https://github.com/jonathanmann/blog_examples/blob/master/recursion_in_haskell/two_to_the_power.hs) that we explored in the [previous post](http://jonathanmann.github.io/2015/02/03/recursion-in-haskell/).

### Naive Implementation

Consider the [naive implementation](https://github.com/jonathanmann/blog_examples/blob/master/recursion_in_haskell/two_to_the_power.hs) :

{% highlight hs %}
two_to_the_power :: Int -> Integer
two_to_the_power 0 = 1
two_to_the_power n = two_to_the_power(n-1) + two_to_the_power(n-1)
{% endhighlight %}

This implementation returns the correct result, but it could be improved to become much faster with memoization.

### Visualization
To understand why the naive implementation is so inefficient consider the following diagram :
![recursion_tree](http://jonathanmann.github.io/public/img/recursion_tree.png)

For every node in the tree, all child nodes must be evaluated in order to return their results to the parent node. Unfortunately, this ends up causing the same problem to be evaluated over and over again across multiple levels. For efficiency, what we would really like to produce is a process that looks more like the following :

![m_recursion_tree](http://jonathanmann.github.io/public/img/m_recursion_tree.png)


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


