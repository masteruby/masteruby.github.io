---
layout: post
title: How to Add Comments to Rails App with Commontator
---

Last time we've added [voting](/weekly-rails/2014/08/05/how-to-add-voting-to-rails-app.html). This time I will show you how easy can be adding comments with Commontator.

## Why to Use Commontator

Commontator has following advantages:

* It includes comments count
* Is easy to configure
* It includes creating, editing and deleting comments
* You can add voting with acts_as_votable
* Is customizable 


## How to Install Commontator

First thing we need to do is to add commontator gem to Gemfile

#### Gemfile

{% highlight ruby %}
gem 'commontator'
{% endhighlight %}

Then install it with Bundler

{% highlight ruby %}
bundle install
{% endhighlight %}

Now you can create Commontator configuration and migrations

{% highlight ruby %}
rake commontator:install
{% endhighlight %}

And move migrations to database

{% highlight sh %}
rake db:migrate
{% endhighlight %}

## How to Use Commontator in Our Models

Let's assume you've got two models, first is **User** and second is a **Link**

User should be able to post comments, so add this line to your User model.

#### app/models/user.rb

{% highlight ruby %}
class User < ActiveRecord::Base
  
  acts_as_commontator
{% endhighlight %}

We want to show comments under each link, so add acts_as_commontable helper to Link model.

#### app/models/link.rb

{% highlight ruby %}
class Link < ActiveRecord::Base

acts_as_commontable
{% endhighlight %}

## Adding Comment's route

Next thing we need to is to add commontator's route.

#### config/routes.rb

{% highlight ruby %}
mount Commontator::Engine => '/commontator'
{% endhighlight %}

## Showing Comments

So we've added commontator's helpers to our model, so we can add commontator's thread to our views. Let's assume we've got index action in links_controller.

#### app/controllers/links_controller.rb

{% highlight ruby %}
class LinksController < ApplicationController

def index
  @links = Link.all
end
{% endhighlight %}

Let's add commontator's thread to our views.

#### app/views/links/index.html.slim

{% highlight html %}

- @links.each do |link|
  = commontator_thread(link)
{% endhighlight %}

Now you should see comments count:

![how to add comments count in Rails](/images/comments-count.png)

Click on show comments, you should see new comment link.

![how to add new comment in Rails](/images/new-comment.png)

Fill in new comment form and look at the comment that we've created:

![how to show comment in Rails](/images/showing-comment.png)

Looks nice isn't it?

## Replacing "Anonymous" with username

You certainly noticed that when you've created comment, it shows Anonymous instead of username.

Let's fix that. Find this line in commontator initializer

#### config/initializers/commontator.rb

{% highlight ruby %}

config.user_name_proc = lambda { |user| I18n.t('commontator.anonymous') }
{% endhighlight %}

Now if you have column username in users table replace previous line with following:

{% highlight ruby %}
config.user_name_proc = lambda { |user| user.username }
{% endhighlight %}

Now if you look at your comments in a browser you should see user's name instead of Anonymous.

## Customization

Let's assume you want to customize views. Run this command:

{% highlight sh %}
rake commontator:copy:views
{% endhighlight %}

You should see that commontator folder was created in our views folder.

That's all for now. I hope that you liked my tutorial. If you don't understand anything about post, feel free to ask in discussion. And if you like it, share it with your favorite social network.

