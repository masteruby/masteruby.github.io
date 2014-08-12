---
layout: post
title: How to Add User Karma in Rails
---

A week ago you've learned [how to add voting](/weekly-rails/2014/08/05/how-to-add-voting-to-rails-app.html). Acts_as_votable is great, but it doesn't provide user karma. This time you will learn how to add user karma functionality to your app.

## What do you need

* Links controller and model created
* User authentication created
* Acts_as_votable gem

## Adding karma column to users table

To use karma for user, we need to generate new migration. Create new migration like this:

{% highlight sh %}
rails generate migration AddKarmaToUsers
{% endhighlight %}

Let's edit it now.

#### db/migrate/add_karma_to_users.rb

{% highlight ruby %}
class AddKarmaToUsers < ActiveRecord::Migration
  def change
    add_column :users, :karma, :integer, :default => 0
  end
end
{% endhighlight %}

This code will add new column to users table with name karma. We've choosed basic type integer and set default value to 0.

Let's migrate it:

{% highlight sh %}
rake db:migrate
{% endhighlight %}

## Adding user as voter

Before we'll use user's karma we need to add another acts_as_votable helper. I'll explain why soon. 

#### app/models/user.rb

{% highlight ruby %}
class User < ActiveRecord::Base
  
  acts_as_voter
  has_many :links
{% endhighlight %}

## Creating methods for increasing and decreasing user's karma

For better readability we'll use separate methods for increasing and decreasing user's karma in user's model.

#### app/models/user.rb

{% highlight ruby %}
class User < ActiveRecord::Base
  has_many :links 
  acts_as_voter
  
  def increase_karma(count=1)
    update_attribute(:karma, karma + count)
  end
{% endhighlight %}

Here we've set method that will update user's karma from default to 1. You will use similar for decreasing.

#### app/models/user.rb

{% highlight ruby %}
def decrease_karma(count=1)
  update_attribute(:karma, karma - count)
end

{% endhighlight %}

We've added methods to models, let's go to controllers.

## Adding user karma to controller

Now we can use user's methods in our links_controller

#### app/controllers/links_controller.rb

{% highlight ruby %}
def upvote
  @link = Link.find(params[:id])
  if current_user.voted_for? @link
    redirect_to links_path
  else
    @link.upvote_by current_user
    @link.user.increase_karma
    redirect_to links_path
  end
end
{% endhighlight %}

Let's check out what we've done.

{% highlight ruby %}
@link = Link.find(params[:id])
if current_user.voted_for? @link
  redirect_to links_path
{% endhighlight %}

First we'll find our link. Then we'll checkout if current signed user has already voted for link, that's why we've used acts_as_voter helper in our User model. If he has we'll just redirect to path with all of links.

{% highlight ruby %}
@link.upvote_by current_user
@link.user.increase_karma
redirect_to links_path
{% endhighlight %}

First we'll upvote link using acts_as_votable as in last time. Then we'll increase karma to user that have created link.

Don't forget to add similar code to downvote action too.

#### app/controllers/links_controller.rb

{% highlight ruby %}

def downvote
  @link = Link.find(params[:id])
  if current_user.voted_for? @link
    redirect_to links_path
  else
    @link.downvote_by current_user
    @link.user.decrease_karma
    redirect_to root_path
  end
end

{% endhighlight %}

## Showing user's karma

Now you can show user's karma in your view too. Let's assume you have got show action in controller like this:

#### app/controllers/users_controller.rb

{% highlight ruby %}
def show
  @user = User.find(params[:id])
end
{% endhighlight %}

Now you can easy display user's karmain your view like this:

{% highlight html %}
= @user.karma
{% endhighlight %}

That's all for now, if you like it, don't forget to share this article with your favorite social network.
  
   
