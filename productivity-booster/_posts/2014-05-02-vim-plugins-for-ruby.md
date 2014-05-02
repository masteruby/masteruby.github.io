---
title: Vim for Rubyist&#58; 10 useful vim plugins for Ruby
layout: post
---

In this post I want to show some useful Vim plugins, that are true productivity boosters for every Ruby programmer. You can install them by either [Pathogen](https://github.com/tpope/vim-pathogen) or [Vundle](https://github.com/gmarik/Vundle.vim).

## 1. [Vim-Rails](https://github.com/tpope/vim-rails)

Vim-Rails plugin is must for every Rails Developer working in Vim. Here's what I've found useful:

### Easy navigation

Want to find some file but don't know its path? Try to use **:find** command:

{% highlight sh %}
:find schema.rb
{% endhighlight %}

You can also move up in your Rails application by finding related files. For example, let's assume you're editing **home.html.slim**. Try to find related file

{% highlight sh %}
:R
{% endhighlight %}

You should see that you're in file **static_pages_controller.rb** and that you have cursor at method named home.

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

Here are commands for editing your layouts, stylesheets and models:

{% highlight sh %}
:Elayout header
:Emodel User
:Estylesheet main
{% endhighlight %}

### Generator Commands

So you want to run migration, generate model or controller. Before vim-rails plugin you have to close your vim session and go back to terminal, not anymore. Here's useful commands you should know. Let's assume you're building model named User, you can simply create model with :Rgenerate and destroy model with :Rdestroy.

{% highlight sh %}
:Rgenerate model User
:Rdestroy model User
:Rserver
{% endhighlight %}

To run rails server within background of Vim you will use Rserver command. 
### Syntax highlighting

Of course syntax highlighting is included too. Vim-rails has built syntax highlighting for special Active Record methods and all keywords that Rails has unique.

That's only small part of what plugin provides, to see list of all commands, go to [project documentation](https://raw.githubusercontent.com/tpope/vim-rails/master/doc/rails.txt). For example, it provides commands forrefactoring your code, it has built support for Rake and other.

## 2. [NerdTree](https://github.com/scrooloose/nerdtree)

Navigation by vim-rails plugin can be great, but only when you know what you're looking for. For other purposes, you can use **NERDTree** as file navigator. 

Type this into vim session to run NerdTree:

{% highlight sh %}
:NERDTree
{% endhighlight %}

You should see content of current working directory. NerdTree use vim navigation keys to move up and down to directory tree.

<img class="vim" src="/images/nerd_tree.png" alt="nerd tree"></img>

Let's assume you want to open up directory **app**. Navigate to app with Vim and press key **o**. You should see content of app directory:

<img class="vim" src="/images/nerd_tree_app.png" alt="nerd tree app"></img>

## 3. [Vim-fugitive](https://github.com/tpope/vim-fugitive)

If you have your project tracked with Git, switching between terminal sessions can be really painful. Fugitive is absolutely greatly tool for using Git inside Vim.

For example let'see what's changed with git status
{% highlight sh %}
:Git status
{% endhighlight %}

Let's add changes to repository
{% highlight sh %}
:Git add .
{% endhighlight %}

Let's push it to origin master
{% highlight sh %}
:Git push origin master
{% endhighlight %}

## 4. [Vim-Ruby](https://github.com/vim-ruby/vim-ruby)

Vim-Ruby provides useful things like easy navigation and syntax highlighting in ruby

Here's list of useful navigation methods in vim-ruby

{% highlight sh %}
# To edit start of next method definition
]m
# To go to end of next method definition
]M
# To start of previous method definition
[m
# To end of previous method definition
[M
{% endhighlight %}


## 5. [Vim-Bundler](https://github.com/tpope/vim-bundler)

You don't have exit vim or attach another tmux session to install gems anymore. Just run :Bundle in command mode in Vim and gems will be installed:

{% highlight sh %}
:Bundle
{% endhighlight %}

To edit Gemfile you will use this command:

{% highlight sh %}
:Bopen
{% endhighlight %}

## 6. [Vim-Cucumber](https://github.com/tpope/vim-cucumber)

Vim-Cucumber plugin provides syntax highlighting and indentation for Cucumber.

## 7. [Vim-slim](https://github.com/slim-template/vim-slim)/[Vim-haml](https://github.com/tpope/vim-haml)

Here's the plugin that provides syntax highlighting for your favorite template language, it can be haml or slim.

## 8. [Vim-Vroom](https://github.com/skalnik/vim-vroom)

With Vroom you can run your tests inside Vim. Supports Rspec, Cucumber and MiniTest. You can run your tests with:

{% highlight sh %}
:VroomRunTestFile
{% endhighlight %}

## 9. [Vim-endwise](https://github.com/tpope/vim-endwise)

Here's the useful plugin that adds end after if, do, def keywords.

## 10. [Supertab](https://github.com/ervandew/supertab)

Supertab is useful in situations when you have lot of repetiting words like **def**. It works that you press Tab and it completes word for you.

If you like this post, share it with clicking on social network toolbar at the top of page. 


