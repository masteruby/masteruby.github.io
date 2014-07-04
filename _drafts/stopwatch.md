---
layout: post
title: How to create stopwatch in Ruby Shoes
---

Last time we've created [digital clock](/shoes/2014/06/29/how-to-create-clock-in-ruby-shoes.html) using Time Library. Today we'll create stopwatch.

Here's how final version will be look like:

<img class="shoes" alt="how to createstopwatch in Ruby" src="/images/stopwatch.png">

* First we'll reset Time to zero
* Then we'll add buttons for startingand reseting our stopwatch.


## Adding reseted time

First thing we need to do is to reset our time, because we want to start from zero.

{% highlight ruby %}
Shoes.app do
  @stopwatch = title ''
  t = Time.new(0)
  @stopwatch.text = t.strftime("%H:%M:%S")
end
{% endhighlight %}

Here's how app looks right now:

<img class="shoes" alt="how to reset time in ruby" src="/images/reset-time.png">

As in the last tutorial we'll start with creating empty title element.

Last time we've used new instance of Time class to save current time. Here we want to reset current time to zero, so we've added zero in parentheses.

And on last line we've converted time to string and add to our title.

## Adding buttons for starting and reseting stopwatch

We want from our stopwatch to start when we press start button and stop when press stop button.

So first we'll create start button.

Add this code:

{% highlight ruby %}
button "Start" do
  animate(1) do
    t += 1
  end
end
{% endhighlight %}

We want to add every second

{% highlight ruby %}
button "Stop" do
  t = Time.new(0)
  @stopwatch.text = t.strftime("%H:%M:%S")
end
{% endhighlight %}

Here we've reset our time again to zero.

Here's the final code:

{% highlight ruby %}
require 'green_shoes'

Shoes.app do
  @stopwatch = title ''
  t = Time.new
  @stopwatch.text = t.strftime("%H:%M:%S")
  
  button "Start" do
    animate(1) do
    @stopwatch.text = t.strftime("%H:%M:%S")
    end
  end
  
  button "Stop" do
    t = Time.new(0)
    @stopwatch.text = t.strftime("%H:%M:%S")
  end
end
{% endhighlight %}

I hope that you like my article, if you like it share it with clicking on buttons on the left sidebar.

