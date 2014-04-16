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
instructions about [how to install
ruby](http://masteruby.github.io/learning-resources/2014/03/28/ruby-on-rails) in previous post.

If you have ruby installed by rvm, just install green_shoes like this:

{% highlight sh %}
$ gem install green_shoes
{% endhighlight %}

## Running shoes

To run we need to add green_shoes gem to our ruby file.

Go to your favorite text editor and type something like this:

#### calculator.rb

{% highlight ruby %}
require 'green_shoes'

Shoes.app(title: "My calculator", width: 200, height: 240) do
end
{% endhighlight %}

Go to the terminal and run calculator.rb. You should see something like this:

![how to run shoes](/images/running_shoes.png)

## Adding basic template for app

Let's add template for our calculator. We need to add place for number field,
clear button and remaining buttons.

{% highlight ruby %}
require 'green_shoes'

Shoes.app(title: "My calculator", width: 200, height: 240) do
  flow width: 200, height: 240 do
    flow width: 0.7, height: 0.2 do
      background rgb(0, 157, 228)
    end

    flow width: 0.3, height: 0.2 do
    end

    flow width: 1.0, height: 0.8 do
      background rgb(139, 206, 236)
    end
  end
end
{% endhighlight %}

If you go run shoes again, you should something like this:

![template for calculator](/images/template.png)

Let's look at what we've done.

First we've created flow, who copy size of screen
{% highlight ruby %}
  flow width: 200, height: 240 do
{% endhighlight %}

Our app is divided into three parts: number field, clear button and remaining buttons, so we've created three different flows to match it. 

{% highlight ruby %}
flow width: 0.7, height: 0.2 do
  background rgb(0, 157, 228)
end
{% endhighlight %}

Here we used floating points to match size of flow. If you type 0.7 it means 70% width of screen and if you type 0.2 it means 20% size. Then we've used background method to change color of the flow.

Ok we've done with preparations, let's create some buttons.



## Adding calculator buttons

First we need to add number field:

{% highlight ruby %}

require 'green_shoes'

Shoes.app(title: "My calculator", width: 200, height: 240) do
  number_field = nil
  @number = 0
  flow width: 200, height: 240 do
    flow width: 0.7, height: 0.2 do
      background rgb(0, 157, 228)
      number_field = para @number, margin: 10
    end
    
    flow width: 0.3, height: 0.2 do
    end    

    flow width: 1.0, height: 0.8 do
      background rgb(139, 206, 236)
    end
  end
end
{% endhighlight %}

So if you run code you should number 0 in number field: 

![number field](/images/number_field.png)

Let's take a look at code:

{% highlight ruby %}
  number_field = nil
  @number = 0
{% endhighlight %}

Here we've set two variables. Variable **number_field** is for displaying number field. In variable **@number** we set actual value of number in calculator.

{% highlight ruby %}
number_field = para @number, margin: 10
{% endhighlight %}

Here we've changed number field to para. Para is method in shoes for displaying text or numbers in screen. We've used **@number** to set para to 0, but it can be anything you like. After that we've set margin to all sizes.

### Adding Clr Button

Now we have to add clr button. To add button type something like this:

{% highlight ruby %}
require 'green_shoes'

Shoes.app(title: "My calculator", width: 200, height: 240) do
  number_field = nil
  @number = 0
  flow width: 200, height: 240 do
    flow width: 0.7, height: 0.2 do
      background rgb(0, 157, 228)
      number_field = para @number, margin: 10
    end
    
    flow width: 0.3, height: 0.2 do
      button 'Clr', width: 1.0, height: 1.0 do
      end
    end    

    flow width: 1.0, height: 0.8 do
      background rgb(139, 206, 236)
    end
  end
end
{% endhighlight %}

{% highlight ruby %}
button 'Clr', width: 1.0, height: 1.0 do
end
{% endhighlight %}

So here we've added button with name **Clr** and set it's width and height to size of flow. 

## Adding remaining buttons

We need to add all buttons what we need. Add code something like this inside third flow.

{% highlight ruby %}

require 'green_shoes'

Shoes.app(title: "My calculator", width: 200, height: 240) do
  number_field = nil
  @number = 0
  flow width: 200, height: 240 do
    flow width: 0.7, height: 0.2 do
      background rgb(0, 157, 228)
      number_field = para @number, margin: 10
    end
    
    flow width: 0.3, height: 0.2 do
      button 'Clr', width: 1.0, height: 1.0 do
      end
    end    

    flow width: 1.0, height: 0.8 do
      background rgb(139, 206, 236)
      %w(7 8 9 + 4 5 6 - 1 2 3 / 0 . = *).each do |btn|
        button btn, width: 50, height: 50 do
        end
      end      
    end
  end
end

{% endhighlight %}

{% highlight ruby %}
%w(7 8 9 + 4 5 6 - 1 2 3 / 0 . = *).each do |btn|
  button btn, width: 50, height: 50 do
  end
{% endhighlight %}

We've added all buttons to array with %w method and added every button to each loop, then we setup height and width of the buttons.

## Running Buttons

So are buttons now displayed, but if you click at them it doesn't work. Let's fix it. Go to clr button and add code something like this.

{% highlight ruby %}
require 'green_shoes'

Shoes.app(title: "My calculator", width: 200, height: 240) do
  number_field = nil
  @number = 0
  flow width: 200, height: 240 do
    flow width: 0.7, height: 0.2 do
      background rgb(0, 157, 228)
      number_field = para @number, margin: 10
    end
    
    flow width: 0.3, height: 0.2 do
      button 'Clr', width: 1.0, height: 1.0 do
        @number = 0
        number_field.replace(@number)
      end
    end    

    flow width: 1.0, height: 0.8 do
      background rgb(139, 206, 236)
      %w(7 8 9 + 4 5 6 - 1 2 3 / 0 . = *).each do |btn|
        button btn, width: 50, height: 50 do
        end
      end      
    end
  end
end

{% endhighlight %}

{% highlight ruby %}
@number = 0
number_field.replace(@number)
{% endhighlight %}

Here we added block of code to button, that every time button Clr is pressed variable @number is set to. Then we use special ruby method **replace** to change actual value of number_field to 0. Maybe it doesn't seems to work, but try change value of variable @number to any other number and then press clr. It should change to zero.

Ok we've added functionality to Clr button let's move on numbers. Inside this block of code inside flow:

{% highlight ruby %}
require 'green_shoes'

Shoes.app(title: "My calculator", width: 200, height: 240) do
  number_field = nil
  @number = 0
  flow width: 200, height: 240 do
    flow width: 0.7, height: 0.2 do
      background rgb(0, 157, 228)
      number_field = para @number, margin: 10
    end
    
    flow width: 0.3, height: 0.2 do
      button 'Clr', width: 1.0, height: 1.0 do
        @number = 0
        number_field.replace(@number)
      end
    end    

    flow width: 1.0, height: 0.8 do
      background rgb(139, 206, 236)
      %w(7 8 9 + 4 5 6 - 1 2 3 / 0 . = *).each do |btn|
        button btn, width: 50, height: 50 do
          case btn
            when /[0-9]/ 
              @number = @number.to_i * 10 + btn.to_i
          end
          number_field.replace(@number)    
        end
      end      
    end
  end
end
{% endhighlight %}

{% highlight ruby %}
case btn
  when /[0-9]/ 
    @number = @number.to_i * 10 + btn.to_i
end
number_field.replace(@number)
{% endhighlight %}

Here we use case to instead bla bla.

After that we've used when with regular expression that match every number from zero to nine. After that we converted number and btn to integers and finally we've used replace method to replace number_field with actual number.

## Adding operations

We have working number buttons, but what to do with operators.

First we need to add two variables, **@previous** and **@op** right after variable **@number**

{% highlight ruby %}
...

@op = nil
@previous = 0

...
{% endhighlight %}





  









