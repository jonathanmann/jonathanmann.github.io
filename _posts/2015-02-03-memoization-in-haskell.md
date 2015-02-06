---
layout: post
title: Stepping Through Memoization in Haskell
---

To better understand how memoization works with Haskell's lazy evaluation, let's walk through a simple example step by step. As a learning tool, we'll create a simple function that raises the number two to a the power of whatever number is given as input. Let's begin with a naive implemenation to get a better idea of what's going on.

### A Naive Implementation

Consider the following code :

{% highlight hs %}

naive_recursive_two_to_the_power :: Int -> Integer
naive_recursive_two_to_the_power 0 = 1
naive_recursive_two_to_the_power n = naive_recursive_two_to_the_power(n-1) + naive_recursive_two_to_the_power(n-1)

{% endhighlight %}

Let's walk through the code line by line.
{% highlight hs %}naive_recursive_two_to_the_power :: Int -> Integer{% endhighlight %}
The first line indicates that the function "naive_recursive_two_to_the_power" will take in datatype Int and return the datatype Integer. The difference between these two datatypes has to do with the maximum size of the integer that the datatype can store. For our purposes, you can simply think of both types as integers, but a detailed explanation can be found [here](http://stackoverflow.com/questions/17766424/dubious-int-vs-integer-handling-in-haskell).

### Tables

Aenean lacinia bibendum nulla sed consectetur. Lorem ipsum dolor sit amet, consectetur adipiscing elit.

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Upvotes</th>
      <th>Downvotes</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Totals</td>
      <td>21</td>
      <td>23</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>Alice</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td>4</td>
      <td>3</td>
    </tr>
    <tr>
      <td>Charlie</td>
      <td>7</td>
      <td>9</td>
    </tr>
  </tbody>
</table>

Nullam id dolor id nibh ultricies vehicula ut id elit. Sed posuere consectetur est at lobortis. Nullam quis risus eget urna mollis ornare vel eu leo.

-----

Want to see something else added? <a href="https://github.com/poole/poole/issues/new">Open an issue.</a>
