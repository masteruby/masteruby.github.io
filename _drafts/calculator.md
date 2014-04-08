---
layout: post
title: How to create simple calculator in Shoes
---

In this tutorial we'll cover:

* How to install Shoes
*
*
*

## How to install Shoes

Before you can install green_shoes you have to install ruby. I've included
instructions about [how to install ruby](http://example.com) in previous post.

If you have ruby installed by rvm, just install green_shoes like this:

{% highlight sh %}
$ gem install green_shoes
{% endhighlight %}

## Running shoes

To run we need to add green_shoes gemto our ruby file.

Go to your favorite text editor and type something like this:

{% highlight ruby %}
require 'green_shoes'
Shoes.app title: "My calculator" do
end
{% endhighlight %}

Go to the terminal and run calculator.rb. You should see something like this:

![how to run shoes](/images/running_shoes.png)

## Adding calculator buttons

Let's add calculator buttons. Insert this code into Shoes.app do block:

{% highlight sh %}
require 'green_shoes'
Shoes.app title: "My calculator" do
  **%w(7 8 9 / 4 5 6 * 1 2 3 + 0 - =).each do |but|**
    **button but**
    end
  end
  {% endhighlight %}

  We've added each button to array and use special **button method** from Shoes
  class.

  You can see result right here:

  ![creating buttons in shoes](/images/creating_buttons.png)

  Our buttons are small and not in ordered let's try to style it. To change
  size of element you will use width and height shoes methods.

 Let's add some code to our app

 {% highlight ruby %}
 require 'green_shoes'
 Shoes.app title" "My calculator" do
 %(7 8 9 / 4 5 6 * 1 2 3 + 0 - =).each do |but|
  button but, **:width => 40, height:40**
  {% endhighlight %}

  


