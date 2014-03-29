---
layout: post
---
In this post I want to show you how to install Rails for your operating system.

##  How to install Ruby and Rails

###  Windows

 Get installer on [rails installer site](http://www.railsinstaller.org/en).
 It will install Ruby with Rails and all dependencies you will use in
 developing Rails application

 Try checking succesfull installation.  Go to the Start Menu, select Accessories and choose Command prompt.

 You should see window with your Windows Version and actual directory path. Let's check it out if Ruby is properly installed. Type this into command prompt:

 {% highlight sh %}
 $ ruby -v
 $ rails -v
 {% endhighlight %}

You should see something like this:

![ruby-on-rails-installation](/images/rails_installation.png)

###  Mac OS X
Start on [rails installer  site](http://www.railsinstaller.org). Now open the Terminal and check if ruby is installed with following command.

{% highlight sh %}
 $ ruby -v
 {% endhighlight %}

 
 You should see the following result:

 {% highlight sh %}
 $ ruby 2.0.0p247
 {% endhighlight %}

 If you want to install Rails by command line try this guide:

 [how to install rails on  mac](http://railsapps.github.io/installrubyonrails-mac.html)

###  Linux

  Start with your package management system. You need to install all dependencies like this:
 
{% highlight sh %}
$ sudo apt-get install apache2 curl git libmysql-client-dev mysql-server nodejs
{% endhighlight %}



  Then you have to install ruby. I recommend you to install it using RVM
{% highlight sh %}
  $ curl -L https://get.rvm.io | bash -s stable
{% endhighlight %}

  Execute following command, which install all requirements for your operating system
{% highlight sh %}
  $ rvm requirements --autolibs=enable
{% endhighlight %}

  Then you can install Ruby.

{% highlight sh %}
  $ rvm install ruby 2.0.0
{% endhighlight %}

After this you can use ruby and install rails

{% highlight sh %}
  $ rvm use 2.0.0

  $ gem install rails 
{% endhighlight %}

  You can check succesfull installation with following command:
{% highlight sh %}
  $ rails -v
{% endhighlight %}

## What's next

That's all for now. If you want to know more about developing Rails
applications I recommend you [ruby on rails
guide](http://guides.rubyonrails.org/getting_started.html). I wrote post about
[how to create todo list app in
rails](http://masteruby.github.io/weekly-rails/2014/03/22/how-to-create-todo-list-app-static-pages.html),
so if you want you can check it out.
