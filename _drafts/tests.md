---
layout: post
title: How to Run Tests in Vim
---

Last time I've show you some [vim plugins for ruby]()

This time I want to show you how and why you should run your tests inside Vim. We'll use following Vim plugins in this tutorial:

* vim-rspec
* vim-dispatch

## Why to Run Tests inside Vim


## Running tests with Rspec

Running test with vim-rspec is reallyeasy. First let's add some mapping to our .vimrc

### Configuring Rspec

For easy using it's better to use following vim-mappings in vim-rspec.

{% highlight sh %}
map <Leader>t :call RunCurrentSpecFile()<CR>
map <Leader>a :call RunAllSpecs()<CR>
map <Leader>s :call RunNearestSpec()<CR>
map <Leader>l :call RunLastSpec()<CR>
{% endhighlight %}

Maybe you wonder what's **<Leader>** in .vimrc. Leader is default key, default **\**. So we've set .vimrc, so to instead running long functions in command mode in Vim, we've use simple

### Running current spec file with Vim-Rspec

Let's assume you've created feature spec, with name **users** and you wantto run only this spec right now. Before vim-rspec you needed to switch tmux session to run tests or open up new terminal window, not anymore

So to run current spec, just run:
{% highlight ruby %}
\t
{% endhighlight %}

And vim-rspec will take work running rspec
### Running all specs

### Running nearest spec

### Running last spec

## Using Dispatch to Run tests 
