---
layout: post
---


In the following series of posts we gonna create todo list app in rails.
In this tutorial we'll create basic structure of our app. In first part of
tutorial you will learn:

* How to install **Rails**
* How to choose text editor for your operating system
* How to use **Rails** in command line 
* How to use **Bundler** to install gems
* How to use **Cucumber** with **Capybara** to test our pages
* How to create our static_pages(home,about,contact)


## 1 What do you need

* You need to have some basic knowledge of HTML, CSS. If you haven't learn them  yet go to [web tutorial on codecademy](http://www.codecademy.com/tracks/web)

* You need to have basics in Ruby. If you haven't go to [ruby tutorial on codecademy](http://www.codecademy.com/tracks/ruby)

* You need to have ruby and ruby on rails installed. I will explain this in next section

## 2 How to install Ruby

### 2.1 Windows

 Get installer on [rails installer site](http://www.railsinstaller.org/en).
 Go to the Start Menu, select Accessories and choose Command prompt.

 You should see window with your Windows Version and actual directory path. Let's check it out if Ruby is properly installed. Type this into command prompt:

 {% highlight sh %}
 ruby -v
 {% endhighlight %}

### 2.2 Mac OS X
 Start on [rails installer  site](http://www.railsinstaller.org). Now open the Terminal and check if ruby is installed with following command.

{% highlight sh %}
 $ ruby -v
 {% endhighlight %}

 
 You should see the following result:

 {% highlight sh %}
 $ ruby 2.0.0p247
 {% endhighlight %}
### 2.3 Linux

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

## 3 Choosing your text editor

  You write all your ruby programs using text editor.

### 3.1 [Notepad++](http://notepad-plus-plus.org/download/v6.5.3.html)

For Windows  I recommend you this editor. It's free and it includes syntax highlighting and auto completion for ruby. 

### 3.2 [TextMate](http://macromates.com)

  On Mac you can use TextMate. You can download it and install for free.

### 3.3 Gedit

  On Linux you can use gedit.

## 4 Creating basic structure of the app
 
 Ok so you've got your tools in order, so we can start to  create application. Open up terminal window or command prompt if you're on Windows and enter following code:

{% highlight sh %}
$ rails new todo --skip-test-unit
{% endhighlight %}

 This will create rails application named todo. It takes a while. Ok let's check out some folders that we're created.

#### Gemfile

 That's the file that you will use to install all dependencies what you need
 for your applications. They're called gems. Just add name of gem to your
 Gemfile and let Bundler to take care of installation.

#### app/views

 In this folder you place your html templates.

#### app/assets
 
Images, Javascript and CSS files belongs here.

### 4.1 How to use Bundler

After creating rails application you should use Bundler to use all dependencies
what you need. First add name of the gem to your Gemfile, then open up terminal
and add following command:

{% highlight sh %}
$ bundle install
{% endhighlight %}

Let's add some gems to your Gemfile. Open up your Gemfile and add following
gems:

{% highlight ruby %}
gem 'slim-rails'
gem 'capybara'
gem 'cucumber-rails', :require => false
gem 'database_cleaner'
gem 'rspec-expectations'
gem 'selenium-webdriver'
{% endhighlight %}

Install it with Bundler:

{% highlight sh %}
$ bundle install
{% endhighlight %}

### 4.2 Starting our application

To run your application, type this into command line:

{% highlight sh %}
$ rails server

{% endhighlight %}

Go to web browser and type localhost:3000. Your output screen should look like this:

 ![rails-opening-screen](/images/rails-opening-screen.png)

## 5 Creating Static Pages

We have our web server running let's build some pages.

### 5.1 Creating controllers

  {% highlight sh %}
 $ rails generate controller StaticPages home help about --no-test-framework
{% endhighlight %}

 If you open your views folder, you should see that you have new folder named
**static_pages** with some files in it. Go to the **config/routes.rb**, you should see path of our pages that we're created. Type for example, localhost:3000/static_pages into your web browser.

 ![home](/images/home.png)
 
We created StaticPages controller and we can populate our files. Testing every
change in a browser would be tedious. So we gonna need Cucumber and Capybara to
do it for us.

### 5.2 Cucumber
Cucumber lets software developers and shareholders to use simple plain language
to describe features. If you want to know more about Cucumber, try
[CucumberBook](http://www.amazon.com/The-Cucumber-Book-Behaviour-Driven-Development/dp/1934356808)
#### How Cucumber works

 Cucumber works in features which are written in plain text and step definitions which are written in regular ruby code. If you go to your app folder, you should see that folder named features  was created.  

First we need to setup folder structure of Cucumber. Run following command:

{% highlight sh %}
$ rails generate cucumber:install
{% endhighlight %}


 We need to test all our static pages. Open up folder features in your main
 directory and add file **static_pages.feature** into your features directory.

#### static_pages.feature

{% highlight gherkin %}

Feature: Static Pages content

 User should see static pages content

 Scenario Outline: Path testing

    When I visit <Path> path 
    Then I should see following content: <Content>
    
    Examples:
      | Path     | Content | 
      | Home     | Todo    |
      | About    | About   |
      | Help     | Help    |

   


 {% endhighlight %}

 This is how it works. At first line you define your feature, in our example
 StaticPages content. Then you define your steps. Steps always begin with
 keywords: Given,When,Then,And and continue with regular expression. It can be
 any text. Don't forget to surround your text in regular expression like this: **/^some text$/**

 We have our feature defined, let's test it with Cucumber

{% highlight sh %}
 $ cucumber
{% endhighlight %}

 You should see something like this:

 ![failing steps](/images/static-pages-failing-steps.png)
 
 Ok we've saw undefined scenarios and steps let's actually implement it. Open
 up folder step-definitions and create file **static_pages_steps.rb**

#### static_pages_steps.rb

{% highlight ruby %}
When /^I visit Home path$/ do 
  visit 'static_pages/home'
end
{% endhighlight %}

In first line we match name of our step with name in the feature file.
Then we use capybara to visit home path in the browser. Run your test with cucumber. You should see one passing test.

Now we need to test content of our home page. Add this into features/step_definitions/static_pages_steps.rb:

{% highlight ruby %}

Then /^I should see following content: Todo$/ do
  expect(page).to have_content("Todo")
end 

{% endhighlight %}

In first line we match second step with feature file.
On the second line we use **Rspec Expectations** to test content of our home page.

Run cucumber again. You should see failing tests. Of course that test is falling, we don't have content Todo in our templates.

Open up folder app/views/static_pages and edit file named **home.html.slim**.

### 5.3 Why to use Slim

Maybe you wonder why we're using files with slim ending. Slim is a template
language that strips all unnecessary elements as opening and closing tags. For example this is a code in html: 

{% highlight html %}
<html>
  <head>
    <title>My WebPage</title>
  </head>
  <body>
    <h1>My heading</h1>
    <p>My paragraph</p>
  </body>
  </html>

  {% endhighlight %}

  And this is code in Slim:

  {% highlight html %}
  html
    head
     title My WebPage
    body
      h1 My heading
      p My paragraph
   {% endhighlight %}

  You see that Slim code is shorter and easier to read as Html code. 
  Let's return to our file. Replace content of **home.html.slim** with following
  content:

#### home.html.slim

{% highlight html %}
h1 Todo 
 
 {% endhighlight %}

You should see that our test is now passing. Implement this to remaining steps
in our feature file.


#### static_pages_steps.rb(excerpt)

{% highlight ruby %}

When /^I visit About path$/ do
  visit 'static_pages/about'
end

Then /^I should see following content: About$/ do
  expect(page).to have_content("About")
end 

When /^I visit Help path$/ do
  visit 'static_pages/help'
end

Then /^I should see following content: Help$/ do
  expect(page).to have_content("Help")
end
{% endhighlight %}


#### about.html.slim

{% highlight html %}
 h1 About
{% endhighlight %}

#### help.html.slim
{% highlight html %} 
 h1 Help
 {% endhighlight %}

 All our tests are now passing, next step will be implement title tests. Open up
 your **static_pages.feature** file and append following line:

#### static_pages.feature
{% highlight gherkin %}

 And I should see following title: <Title>

 Examples:
   | Path     | Content | **Title |**
   | Home     | Todo    | **Todo  |**
   | About    | About   | **About |**
   | Help     | Help    | **Help  |**
 
{% endhighlight %}

 Let's implement our test. Add these lines to our steps file.

#### static_pages_steps.rb

 {% highlight ruby %}

And /^I should see following title: Todo$/ do
  expect(page).to have_title("Todo")
end

And /^I should see following title: About$/ do
  expect(page).to have_title("About")
end

 And /^I should see following title: Help$/ do
  expect(page).to have_title("Help")
end

{% endhighlight %}

Let's fix failing tests. We need to change our title in our templates.

#### home.html.slim
{% highlight html %}
html
  head
    title Todo
{% endhighlight %}

#### about.html.slim
{% highlight html %}
html
  head
    title About
{% endhighlight %}

#### help.html.slim
{% highlight html %}
html
  head
    title Help
{% endhighlight %}

Let's run cucumber again. You should see that's all our steps are now passing. We are done.

## 6 What to improve

### 6.1 Watching step changes with Guard
There's lot a place to improve. For example running cucumber every time for
every change in terminal it's disgusting. Let's change it. We can use **Guard**
to watch every change in our features folder. Add Guard to your Gemfile.

{% highlight ruby %}
gem 'guard-cucumber' 
{% endhighlight %}

And install it:

{% highlight sh %}
$ bundle install
{% endhighlight %}

Let's run Guard with Cucumber.

{% highlight sh %}
$ guard init cucumber
{% endhighlight %}


If you open your app's folder you should see that file named **Guardfile** was
created.

Let's run Guard to run our features automatically.

{% highlight sh %}
$ guard
{% endhighlight %}

All features are running automatically by now.


### 6.2 Eliminate duplication in title

Take a look at files in views folder.
You saw that we've writed title tag three times. That's terrible, let's do
something about that. First rename file in **app/views/layouts** directory.

{% highlight sh %}
mv application.html.erb application.html.slim
{% endhighlight %}

Delete all content and replace it with following:

#### app/views/layouts/application.html.slim

{% highlight html %}

doctype html
html
  head
    title Todo
    = stylesheet_link_tag    "application", media: "all", "data-turbolinks-track" => true
    = javascript_include_tag "application", "data-turbolinks-track" => true
    = csrf_meta_tags
  body
    = yield
{% endhighlight %}

#### app/views/static_pages/about.html.slim

{% highlight html %}

- provide(:title, 'About')
h1 About
{% endhighlight %}

#### app/views/static_pages/help.html.slim

{% highlight html %}

 - provide(:title, 'Help')
h1 Help
{% endhighlight %}

We're done here. In next tutorial we'll do some styling to our app




    

