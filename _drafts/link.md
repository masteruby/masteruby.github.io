---
layout: post
---

## How to create link aggregation site

In this post we'll create link aggregation that look like **Hacker News**.

Here's how it'll be look like:

![link aggregation site](/images/)

In this tutorial we'll cover:

* Design our page with HTML, CSS
* Creating authentication with Devise
* How to create, edit and delete links
* How to show link user and time whenpost was submitted.

## Design our page

First we creat our app

{% highlight sh %}
rails new mlink
{% endhighlight %}

We'll start with designing how our page will be look like.

Add slim or haml gem to your Gemfile.

#### Gemfile
{% highlight ruby %}
gem 'slim-rails'
{% endhighlight %}

### Creating navigation

We'll start with basic navigation, wewant to show things related to links on left side and authentication on right side. Create controller named home

{% highlight sh %}
rails generate controller home
{% endhighlight %}

Create **home.html.slim** in app/views/home:

#### app/views/home/home.html.slim


```html
#wrapper
  header.navbar

	ul.links 

 	li = link_to "Mlink", '#'
    li = link_to "Home", '#'
    li = link_to "Submit", '#'
    ul.auth
```
		li = link_to "Login", '#'
    li = link_to "Signup", '#'
	section#content
		ol#link
			li
				span.link
					= link_to "Geeklist - social network for geeks", '#'
 				span.details
					p
 						| posted by
						= link_to "ed wood", '#'
						| 20 minutes ago



     








