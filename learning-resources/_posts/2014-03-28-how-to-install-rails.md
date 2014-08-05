---
layout: post
title: How to install Ruby on Rails for your operating system 
---

In this post I want to show you how to install Ruby on Rails.

##  How to install Ruby on Rails on Windows


### Step 1: Get rails installer

 Get installer on [rails installer site](http://www.railsinstaller.org/en).

 ![installing rails on windows step 1](/images/installer.png)

### Step 2: Run rails installer

 Go to folder where you've downloaded installer and run it:

 ![installing rails on windows step 2](/images/rails_installer_setup.png)

 It will install Ruby with Rails and all dependencies you will use in
 developing Rails application

### Step 3: Running installer in Command prompt

 Try checking succesfull installation.  Go to the Start Menu, select all
 programs and choose **Rails Installer** and then **Command Prompt with Ruby
 and Rails**
 
 ![how to install ruby and rails on windows step 3](/images/running.png)


 You should see window with your Windows Version and actual directory path. Let's check it out if Ruby is properly installed. Type this into command prompt:

 {% highlight sh %}
 $ ruby -v
 $ rails -v
 {% endhighlight %}

You should see something like this:

![ruby-on-rails-installation](/images/checking.png)

## How to install Ruby and Rails on Mac OS X

Use either rails installer or go to [this website](http://pragmaticstudio.com/blog/2010/9/23/install-rails-ruby-mac) for
installation instructions


## How to install Ruby on Rails on Linux

### Step 1: Install RVM

RVM(Ruby Version Manager) is a simple tool for easy installation of ruby. First you have to install curl.

{% highlight sh %}
$ sudo apt-get install curl
{% endhighlight %}

Then install rvm:

![how to install ruby and rails on linux step 1](/images/how_to_install_rvm.png)

### Step 2: Installing ruby

Go and install ruby with RVM:

![Installing Ruby and Rails on Linux step 3](/images/ruby_installation.png)

### Step 3: Installing Rails

For installing Ruby on Rails you'll use Rubygems.

![how to install ruby and rails on linux step 3](/images/how_to_install_rails.png)
   

Ok let's check out succesfull installation with terminal:

{% highlight sh %}
$ rails -v
$ ruby -v
{% endhighlight %}

## What's next

That's all for now. If you want to know more about developing Rails
applications I recommend you [ruby on rails
guide](http://guides.rubyonrails.org/getting_started.html). I wrote post about
[how to create todo list app in
rails](http://masteruby.github.io/weekly-rails/2014/03/22/how-to-create-todo-list-app-static-pages.html),
so if you want you can check it out.
