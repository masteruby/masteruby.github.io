---
layout: post
---

In previous part of this tutorial we've created [static pages](http://masteruby.github.io/weekly-rails/2014/03/22/how-to-create-todo-list-app-static-pages.md)

Now we move on adding,removing,editing tasks on our todo rails app.

## Adding tasks

If you want to build some tasks we need to generate another controller. Open
up terminal and type this:

{% highlight sh %}
$ rails generate controller Tasks
{% endhighlight %}

First we'll write some tests. Add file **tasks.feature** to your features
directory.

#### tasks.feature

{% highlight sh %}
Feature: Task Manipulation

Scenario: Adding Tasks
  When I add new task
  Then I should see task added message
{% endhighlight %}

Now write out step_definitions.

#### tasks_steps.rb

{% highlight ruby %}
When /^I add new task$/ do
  fill_in "task_name", with: "Pay a bill"
  click_button "Add tasks"
end  
{% endhighlight %}

Try to run your test with guard. You should see falling test:

![task added test](/images/task_falling.png)

Of course our test is falling. We don't have records in our database and we
don't have task form.

We need to create models to record our tasks to database.

Let's generate Task model in terminal

{% highlight sh %}
rails generate model Task
{% endhighlight %}

Now you can play with your tasks in your in rails console.

{% highlight sh %}
rails console 
{% endhighlight %}





