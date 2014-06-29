---
layout: post
title: How to create digital clock in Ruby Shoes
---

In this post I want to show how to create digital clock using Shoes.

<img class="shoes" src="/images/clock.png" alt="how to create clock in Ruby">

Clock is first in following series of tutorials about using Time library in Shoes. Next time we'll look at stopwatch and timer.

 You can find out example code on [github](https://github.com/MilosDolobac/green-shoes-apps)

Here's what we've in front of us.

* First we'll add current time with Ruby Time library and append in to title element
* Then we'll add automatic update to current time
* And we'll add some styling to our clock

## Adding current Time to our app.

First thing we need to do is add current time. We'll use Time library for this. Create ruby file **clock.rb** and add this code:

{% highlight ruby %}
require 'green_shoes'

Shoes.app height: 50, width: 230 do
  flow margin: 5 do
    @clock = title ''
    t = Time.new
    @clock.text = t.strftime("%H:%M:%S")
  end
end
{% endhighlight %}

If you run our app right now, you should see something like this:

<img class="shoes" src="/images/adding-time.png" alt="adding current time in ruby">

Take look at the code we've just done.

{% highlight ruby %}
@clock = title ''
{% endhighlight %}

We'll store our clock in element title with name **@clock**. We didn't usetitle until now, so you need to know that difference between title and para is that para is 12px high and titleis 34px high. 

{% highlight ruby %}
t = Time.new
@clock.text = t.strftime("%H:%M:%S")
{% endhighlight %}

On a first line we've created instance of Ruby Time class. On second line we've converted only hours, minutes, and seconds to string for using in our title.

## Updating clock

Our clock isn't working well. We want to update clock after every change in time. Updating is very simple. Just add this code.

{% highlight ruby %}
require 'green_shoes'

Shoes.app do
  flow do
    @clock = title ''
    animate do
      t = Time.new
      @clock.text = t.strftime("%H:%M:%S")
    end
  end
end
{% endhighlight %}

Run your app now, it should update clock every second. 


## Adding some style to clock

Our clock isn't looking very good. Let's fix it, replace code with clock text with this:

{% highlight ruby %}
@clock.text = bg(fg(t.strftime("%H:%M:%S"), rgb(0, 255, 0)), black)
{% endhighlight %}

Take last look at the code we've just done:

{% highlight ruby %}
require 'green_shoes'

Shoes.app height: 50, width: 230 do
  flow margin: 5 do
    @clock = title ''
    animate do
      t = Time.new
      @clock.text = bg(fg(t.strftime("%H:%M:%S"), rgb(0, 255, 0)), black)
    end
  end
end
{% endhighlight %}

So here we've set color of clock numbers to green and background to black.

Now we're done. Have some ideas how to improve clock? Feel free to add changes to github.
