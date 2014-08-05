---
layout: post
title: How to Add Voting to Rails App
---

In this post I want to show to add upvotes and dowvotes using **acts_as votable** gem.

## What do You Need

* Basic Authentication with current_user helper(Devise or something else)
* One model with name **Link** and controller links
* acts_as_votable gem installed

## How to setup acts_as_votable

Add gem acts_as_votable to your Gemfile.

#### Gemfile

{% highlight ruby %}
'acts_as_votable'
{% endhighlight %}

And install it with bundle

{% highlight sh %}
bundle install
{% endhighlight %}

Now generate acts_as_votable migration

{% highlight sh %}
rails generate acts_as_votable:migration
{% endhighlight %}

And migrate to database

{% highlight sh %}
rake db:migrate
{% endhighlight %}

Now we're done with preparation let's add upvote action.

## Adding upvotes

First thing we need to is to add acts_as_votable helper to our model.

#### app/models/link.rb

{% highlight ruby %}
class Link < ActiveRecord::Base
  acts_as_votable
end
{% endhighlight %}

Helper will provide useful methods like this:

{% highlight ruby %}
upvote_by ..... => Add upvote by current_user
get_dislikes.size => Count all downvotes
get_likes.size => Count all upvotes
{% endhighlight %}

You can checkout all methods at acts_as_votable documentation.

So now when we know how acts_as_votable can helps us, let's add upvoting to our controller.

#### app/controllers/links_controller.rb 

{% highlight ruby %}
def upvote
  @link = Link.find(params[:id])
  @link.upvote_by current_user
  redirect_to links_path
end
{% endhighlight %}

#### config/routes.rb

{% highlight ruby %}
resources :links do
  member do
    put "like", to: "links#upvote"
    put "dislike", to: "links#downvote" 
{% endhighlight %}

Here we've added two routes, one for upvoting and another for downvoting that will update current like and dislikes size in votes table. 

Now we need to add upvote route to our root path.

#### app/views/links/index.html.slim

{% highlight html %}
- @links.each do |link|
  = link_to "upvote", like_link_path(link), method: :put

{% endhighlight %}

If you click on link, and checkout upvotes size like this in console:

{% highlight sh %}
@link = Link.find(1)
@link.get_upvotes.size => 0
{% endhighlight %}

You certainly noticed that nothing will happen. Of course because voting only counts when we're signed in. Try to signin and now click on link. Now if you checkout in console, everything should work.

{% highlight sh %}
@link = Link.find(1)
@link.get_upvotes.size => 1
{% endhighlight %}

## Adding downvoting

Adding downvoting to rails app is reversed process to upvoting, so instead of **upvote_by** you will add **downvote_by**

#### app/controllers/links_controller.rb

{% highlight ruby %}
def downvote
  @link = Link.find(params[:id])
  @link.downvote_by current_user
  redirect_to links_path
end
{% endhighlight %}

Add path to links path. 

#### app/views/links/index.html.slim

{% highlight html %}

= link_to "downvote", dislike_link_path(link), method: :put
{% endhighlight %}

## Showing link's score

Next thing we need to is to add link's score. Adding score is easy, thanks to methods get_upvotes.size and get_downvotes.size we can just add score method to our model.

#### app/models/link.rb

{% highlight ruby %}
def score
  self.get_upvotes.size - self.get_downvotes.size
{% endhighlight %}

And this to your view file

#### app/views/links/index.html.slim

{% highlight html %}
= link.score
{% endhighlight %}

Now if you click on link, you should see that our score is automatically updated by downvotes and upvotes.

That's all for now, if you don't understand anything, feel free to ask in discussion. 
