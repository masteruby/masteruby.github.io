---
layout: post
---

In previous part of this tutorial we've created [static pages](http://masteruby.github.io/weekly-rails/2014/03/22/how-to-create-todo-list-app-static-pages.md)

In this post we'll learn:

* How to style our app with Bootstrap
* Showing list of all tasks
* Adding tasks
* Deleting Tasks
* Completing Tasks

## Styling our app with Bootstrap

Our app is little bit boring, just html, no css. Let's do something about that we will use Bootstrap to take care of basic design

### Get started with Bootstrap

Bootstrap is a framework for easier developing websites. To use it we have to install **bootstrap-sass** gem

#### Gemfile
{% highlight sh %}
$ gem 'bootstrap-sass'
{% endhighlight %}

{% highlight sh %}
$ bundle install
{% endhighlight %}

### Styling Navigation with Boostrap

Let's make our navigation prettier. Go to the app/views/layouts and add this code right after body.

#### app/views/layouts/application.html.slim

{% highlight html %}
header.navbar
  .navbar-inner
    .container
      nav
        ul.nav.navbar-nav
          li = link_to "Home", root_path
          li = link_to "Help", help_path
          li = link_to "About", about_path
          
{% endhighlight %}

To work we need to import bootstrap from our extended css file. Create file **main.css.scss** in **app/assets/stylesheets** directory.

### What is scss
Scss is improved CSS, it allow us to use variables, and removes some repetitions in our commands. If you want to know more about Sass I recommend you
[pragmatic guide to sass](http://www.amazon.com/Pragmatic-Guide-Sass-Hampton-Catlin/dp/1934356840) book

Add this code to **main.css.scss**

#### app/assets/stylesheets/main.css.scss

{% highlight css %}
@import "bootstrap";
{% endhighlight %}

So we have bootstrap imported,let's look at the home page:

![bootstrap navigation](/images/navigation.png)

So we've applied some styling let's move on showing list of tasks

## Showing list of all tasks

To manipulate tasks we need to create a new controller:

{% highlight sh %}
$ rails generate controller Tasks
{% endhighlight %}

That's fine, but we need to record tasks do database. Writing all sql code would be tedious, fortunately there is **Active Record** to help.

### What is Active Record
Active Record is Object-Relation-Mapping Software, that means that maps row in database to Ruby object. You don't have to write sql, you can use Ruby. If you
want to know more about Active Record you can try [this site](http://guides.rubyonrails.org/active_record_basics.html)

### Creating Models

We need to create models to add records to database.

{% highlight sh %}
$ rails generate model Task name:string
{% endhighlight %}


Our model isn't already in database, we need to move our migration. Go to db/migrate folder. You should see migration **create_tasks.rb**

![rails migration](/images/migration_file.png)

{% highlight sh %}
$ rake db:migrate
{% endhighlight %}

And move it for test purposes.

{% highlight sh %}
$ rake db:test:prepare
{% endhighlight %}

Let's go to rails console and create some tasks. 
{% highlight sh %}
$ rails console
{% endhighlight %}

![creating task in console](/images/creating_task.png)

You saw that we've created task with name **Pay a bill**. That's fine it works in console, but to view it in browser we need to add some code to our controllers and views.

First we'll generate list of all tasks. We want to generate lists of tasks on
home page, so we'll use static_pages_controller, otherwise we would use tasks
route with tasks controller. Go to **app/controllers/static_pages_controller.rb** and add this code.

#### app/controllers/static_pages_controller.rb

{% highlight ruby %}
def home
  @tasks = Task.all
{% endhighlight %}

This code will check all instances of object Task and save it into variable **@tasks**

We want to show all tasks on home page, open up
**app/views/static_pages/home.html.slim** and add following code:

#### app/views/static_pages/home.html.slim

{% highlight html %}

ul#tasks
  - @tasks.each do |task|
    li = task.name
 {% endhighlight %} 

In this code we connect view with static_pages controller and with each method
we loop through all the tasks and add their names to unordered list.

Go to checkout change in browser. You should see list with our recently created tasks.

![task-list](/images/tasks_list.png)

## Adding Tasks

It works, with some problems. Creating task from rails console would be really boring. We need to create task form to do it for us.

First we write up some tests. Create new file **tasks.feature**

#### features/tasks.feature

{% highlight gherkin %}
Feature: Task Manipulation
  In order to use my todo list app I want to add, remove and complete my tasks.
    Scenario: Adding task
    When I add a new task
    Then I should see task added message
{% endhighlight %}

Now write some step definitions.

#### features/step_definitions/tasks_steps.rb

{% highlight ruby %}
When /^I add a new task$/ do
  visit root_path
  fill_in 'task_name', :with => 'Pay a bill'
  expect { click_button "Add task" }.to change(Task, :count).by(1)
end
{% endhighlight %}

We used capybara methods to fill in form for task. fill_in method fills text field **task_name** and click button with value **Add task**, then it count
number of tasks and if one more tasks has been it will pass.

Try it now. Our tests should fail.

![failing form](/images/failing_form.png)

We need to add routes for tasks. To save the time we use resources to generate
all the routes for tasks.

#### config/routes.rb
{% highlight ruby %}
resources :tasks
{% endhighlight %}

Let's try to create our form.

#### app/views/static_pages/home.html.slim

{% highlight html %}
= form_for :task, url: tasks_path do |f|
  = f.label :name
  = f.text_field :name
  = f.submit "Add task", class: "btn btn-large btn-primary"
{% endhighlight %}

Maybe you wonder what **form_for** method does. Take look at this at the browser.

![tasks form](/images/tasks_form.png)

If you look at it with Firebug, Chrome Developer Tools or something like that,
you should see that **form_for** method will create html code as you see in the
picture.

Form is created but it doesn't work because we didn't add controller.

#### app/controllers/tasks_controller.rb

{% highlight ruby %}
def create
 @task = Task.new(task_params)
 @task.save
 redirect_to root_path
 {% endhighlight %}

 Maybe you wonder what means **task_params**. Due to security issues Rails
 developers add some safer code to create new objects.

 Add this code to bottom of the **tasks_controller**

#### app/controllers/tasks_controller.rb

{% highlight ruby %}

 private
  def task_params
    params.require(:task).permit(:name)
    end

{% endhighlight %}    
    

 

We've completed our test let's move on second. We need to add Task added
Message. To display success or error messages with controller we will use flash
hash.

Let's write test first.

#### features/step_definitions/tasks_steps.rb
{% highlight gherkin %}
Then /^I should see task added message$/ do
  expect(page).to have_content "Task added"
end
{% endhighlight %}

Our test should fail. To work we need to add flash notice to our controller and add it to layout.

#### app/controllers/tasks_controller.rb

{% highlight ruby %}
flash[:notice] = "Task added"
{% endhighlight %}

#### application.html.slim

{% highlight html %}
- if notice
  = notice
- if alert
  = alert
{% endhighlight %}  

Try to run test now you should see passing tests. If you go to web browser you should see task added message at the top of the page

![task added](/images/task_added.png)

## Removing Tasks
If we'll complete our tasks we should remove them from tasks list. First we'll write some tests

#### features/tasks.feature

{% highlight gherkin %}
When I delete task
Then I should see task deleted message
{% endhighlight %}

#### features/step_definitions/tasks_steps.rb
{% highlight ruby %}
When /^I delete task$/ do
  visit root_path
  expect { click_button "Delete task" }.to change(Task, :count).by(-1)
end

Then /^I should see task deleted message$/ do
  expect(page).to have_content("Task deleted")
end
{% endhighlight %}

Our tests should fail. We need to add some code to our views and controllers.

{% highlight ruby %}
def destroy
  @task = Task.find(params[:id])
  @task.destroy
  redirect_to root_path
  flash[:alert] = "Task deleted"
 {% endhighlight %} 

This code will find Task by id and saves it to variable and then it will use
Active Record destroy method to remove it.

Add this code to **home.html.slim**

#### app/views/static_pages/home.html.slim

{% highlight html %}
= link_to 'Delete task', task, method: :delete
{% endhighlight %}

If you test it right now. You should see passing tests.

## Completing Tasks

We want to complete tasks and display it as completed. To do it 
we need to add boolean completed to our tasks table.

{% highlight sh %}
rails generate migration AddCompletedToTask
{% endhighlight %}

We need to edit our migration manually. Open up
**db/migrate/add_completed_to_task.rb** and add some content:

#### db/migrate/add_completed_to_task.rb

{% highlight ruby %}
def change
  add_column :tasks, :completed, :boolean
  end
  {% endhighlight %}

 We need to add new route.

#### config/routes.rb
 {% highlight ruby %}
 match 'tasks/complete' => 'tasks#complete' :via => post
 {% endhighlight %}

 And view and controller

#### app/views/static_pages/home.html.slim
 {% highlight html %}
 = form_tag("/tasks/complete", :method => "post") do
  ul#tasks
    - @tasks.each do |task|
      - if task.completed == true
        li[style="color:grey;"]
          = check_box_tag "tasks_checkbox[]",task.id 
          strike
            = task.name
          = link_to 'Delete task', task, method: :delete
          
      - else
        li
          = check_box_tag "tasks_checkbox[]",task.id
          = task.name
          = link_to 'Delete task', task, method: :delete  

  = submit_tag("Complete Task", class: "btn btn-large btn-primary")    
= form_for :task, url: tasks_path do |f|
  = f.label :name
  = f.text_field :name
  = f.submit "Add task", class: "btn btn-large btn-primary"
  {% endhighlight %}
  
  We checkout if task has attribute **completed** set to true and if it does we use strike and little css styling.
  
#### app/controllers/tasks_controller.rb

{% highlight ruby %}

  def complete
    params[:tasks_checkbox].each do |check|
      task_id = check
      t = Task.find_by_id(task_id)
      t.update_attribute(:completed, true)
      flash[:notice] = "Task completed"
    end
    redirect_to root_path
  end
{% endhighlight %} 

## What's next

In next tutorial we'll look at user authentication.

   


  


