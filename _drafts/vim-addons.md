---
title: Vim for Rubyist
layout: post
---

In this post I want to show some useful Vim addons, that are true productivity boosters for every Rails programmer. You can install it by either [Pathogen](https://github.com/tpope/vim-pathogen) or [Vundle](https://github.com/gmarik/Vundle.vim).

## 1. [Vim-Rails](https://github.com/tpope/vim-rails)

Here is the first addon you should try. What I've find useful:

### Easy navigation

Want to find some file but don't know its path? Try to use **:find** command:

{% highlight sh %}
:find Rakefile
{% endhighlight %}

You can also move up in your Rails application by finding related files. For example, let's assume you're editing **home.html.slim**. Try to find related file

{% highlight sh %}
:R
{% endhighlight %}

You should see that you're in file **static_pages_controller.rb** and havecursor at method named home.

### Great Editing

Jumping from views to controllers to models can be really painful. Here's where **vim-rails** plugin excels. For example let's assume you have file named **home.html.slim** in your **views** directory. You can edit it with simple **Eview**:

{% highlight sh %}
:Eview static_pages/home
{% endhighlight %}

You see? You don't have to
set file extension or whole path, just add name of your controller and name of your view file.

Similarily you can edit controller too:

{% highlight vim %}
:Econtroller static_pages
{% endhighlight %}

Here's list of remaining editing commands you will use:

{% highlight sh %}
:Elayout header
:Emodel User
:Estylesheet main
{% endhighlight %}

### Generator Commands

So you want to run migration, generate model or controller. Before vim-rails plugin you have to either close your vim session and go to terminal, not anymore. Here's useful commands you should know. Let's assume you're building model named User, you can simply create model with :Rgenerate and destroy model with :Rdestroy.

{% highlight sh %}
:Rgenerate model User
:Rdestroy model User
:Rserver
{% endhighlight %}

To run rails server within background of Vim you will use Rserver command. 
### Syntax highlighting

Of course syntax highlighting is included too. Vim-rails has built syntax highlighting for special Active Record methods and all keywords that Rails has unique.

That's only small part of what pluginprovides, to see list of all commands, go to [project documentation](https://raw.githubusercontent.com/tpope/vim-rails/master/doc/rails.txt)

## 2. [Vim-Bundler](https://github.com/tpope/vim-bundler)

You don't have exit vim or attach another tmux session to install gems anymore. Just run :Bundle in command mode in Vim:

{% highlight sh %}
:Bundle
{% endhighlight %}

To edit Gemfile you will use this command:

{% highlight sh %}
:Bopen
{% endhighlight %}

### 3. [Vim-Cucumber](https://github.com/tpope/vim-cucumber)

Vim-Cucumber plugin provides syntax highlighting and indentation for Cucumber.

### 4. [Vim-slim](https://github.com/slim-template/vim-slim)[Vim-haml](https://github.com/tpope/vim-haml)

Here's the plugin that provides syntax highlighting for your favorite template language, maybe it is erb, slim or haml.

### 5. [Vim-rake](https://github.com/tpope/vim-rake)

### 6. [Vim-fugitive](https://github.com/tpope/vim-fugitive)

If you have your project tracked with Git, switching between terminal sessions can be really painful. What about
{% highlight sh %}
:git
{% endhighlight %}

### 7. [Vim-endwise](https://github.com/tpope/vim-endwise)

Here's the useful plugin that adds end after if, do, def keywords.



### 8. [Vim-Ruby](https://github.com/vim-ruby/vim-ruby)

### 9. [NerdTree](https://github.com/scrooloose/nerdtree)

Navigation by vim-rails plugin can be great, but only when youknow what you're looking for. For other purposes, you can use **NERDTree** absolutely great file navigator.

Open up and type this into vim session:

{% highlight sh %}
:NERDTree
{% endhighlight %}

You will see something like this:

<img class="vim" src="/images/nerd_tree.png" alt="nerd tree"></img>

Let's assume you want to open up directory **app**. Navigate to app with Vim and press key **o**. You should see content of app directory:

<img class="vim" src="/images/nerd_tree_app.png" alt="nerd tree app"></img>



