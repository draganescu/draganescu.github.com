---
layout: post
title:  "Introducing RasterPHP"
date:   2014-06-29 10:18:00
categories: Raster specs PHP
excerpt: RasterPHP brief introduction.
---

###a framework even designers can understand ^-^

Technical g[uy|irl]? here is the [annotated source code](http://raster-docs.herokuapp.com/sm/)

Ok, this has to be appreciated at least for the nerve — making a PHP framework in 2014, the year of the node, is both uncool and hard to promote. But you’re here, and so please carry on, you might be impressed.

Raster PHP is a super small footprint collection of ideas — that are weaved up together in a cloth of magic coding happiness.

This is a framework for web sites, not for web apps. For web apps you probably don’t even need a PHP framework anyway — because if you make it in PHP you’re gonna be the laughing stock of all your nerdy friends …., just think about it — the horror! O_O

However what makes Raster PHP stand apart is the awesome comments based templating engine that does not break the layout, nor does it kill the dummy content. This is made possible via magic and some little used model view controller variant named MVC-pull.

A standard view in Raster PHP is along the lines of the below example:

{% highlight html %}
<html>
  <!-- res.head_part -->
  <head>
    <title>Welcome</title>
  </head>
  <!-- /res.head_part -->
  <body>
    <h1>A list of things</h1>
    <!-- render.tasks.list -->
     <p>
       <!-- print.task_name -->
         Lorem ipsum
       <!-- /print.task_name -->
     </p>
    <!-- /render.tasks.list -->
  </body>
</html>
{% endhighlight %}

What this simple view does is the following two things:

Creates a reusable part named head_part which can be called in other views
Loads a plain php class named tasks and calls its list method
Raster PHP, like any modern framework, is based on a set of conventions but, unlike some modern frameworks, makes those conventions configurable. In our example above tasks is a plain straightforward PHP class:

{% highlight php %}
<?php
class tasks
{
 
  function list()
  {
    return array(
     array(
      “task_name” => “Walk the dog”
     ),
     array(
      “task_name” => “Fill in groceries list”
     ),
     array(
      “task_name” => “Convince people to use Raster”
     ),
    );
  }
 
}
{% endhighlight %}

This simple example will output the list of tasks as the model offers them. In Raster PHP the model always returns only data which the view uses to update itself. In this case the array will produce this result:

{% highlight html %}
<html>
 <head>
   <title>Welcome</title>
 </head>
 <body>
   <h1>A list of things</h1>
   <p>
     Walk the dog
   </p>
   <p>
     Fill in groceries list
   </p>
   <p>
     Convince people to use Raster
   </p>
 </body>
</html>
{% endhighlight %}

Yes, its that simple. The models can do anything that can be done with PHP, connect to databases, load files, calculate the EBITDA of your next venture — the works. The views are plain HTML with some comments that execute the models you tell them to and show the data nicely formatted.

With Raster PHP you can do many other things, but they are all completely optional:

- use plain SQL as a form of pseudo-ORM
- manage forms in all their glory, with auto field value completion
- have an API that others can use
- make a full blown CMS
- All of the features are documented (mostly) with annotated source code that walks you step by step trough the logic of how a Raster app works. But you needn’t know that necessarily.

<blockquote>
You could have your PSD2HTML and comment your way in them based on the logic above, then have some dev implement the PHP side.
</blockquote>

###Wait, there’s more good stuff

####Does it work?
I have used it in personal projects but also production quality websites and so far it behaved very well showing no drawbacks. Since its all about fast string operations and a few loaded files the performance of Raster PHP turbo style ☺

####Raster PHP is portable
The first version of Raster PHP, named Spartan PHP because, well, it was so spartan, is ported to both Code Igniter and Wordpress. I am mentioning these, which are old unmaintained projects, just to note the flexibility of Raster PHP — one can easily encapsulate all the nice in it and also use the heavy power of big frameworks or apps but, at the same time, achieve the beauty of html comments templates.

####Raster PHP is fully event based
Everything the framework does from detecting what view to load for some URL (routing) to executing template parsing and models fires events. You can easily hook to these events and change the way everything works in one line of code:

`event::bind(‘some_event’)->to(‘model’,’method’);`


Raster PHP has powerful templating
In the example above only render was shown but raster has a wide selection of ways to output data in views such as:

`<!-- print.model.method -->
<!-- print.if.variable -->
<!-- print.@attribute.variable -->
<!-- print.+attribute.variable -->
<!-- dry.view.res_name -->
`

etcetera!

These other template tags offer a completely flexible way to think about your website using MVC-pull:

- print will output data as a string wherever you place it
- print.@ and print.+ will output data inside HTML attributes
- print.if will now show if the variable you specify is false
- dry will bring parsed resources from other views
- etcetera means there is a lot more ☺

####Raster PHP uses RedBean and SQL
RedBean is a one of a kind ORM that allows you do connect and operate any kind of database without any kind of advanced functionality. But a model in Raster PHP will allow you to call simple SQL as overloaded methods of the database class with arguments.

####Raster PHP comes with various ready made models
Although a work in progress, porting them from an older version, Raster includes a basic CMS model that works on any content, a pagination class, auto API, i18n, validation and so on.

Raster PHP is a framework that adheres to the microPHP manifesto and because of that your projects will be more fun and less spaghetti!

###What’s next

With this article i am opening a series on Raster with the hope of spreading the word about a clear and definitely useful way of building dynamic websites: using Raster PHP.

If you want to know more don’t hesitate to contact me @andraganescu.

If you want to use the power of the fork … even better, contributors are welcome with open arms contact me @andraganescu or visit this Github user.

Hopefully this will not make you leave Laravel in the gutter, because that will cost you your artisan status, but it will open up another nice choice for use when the project you are working on might be crushed under the grangantuan weight of a fully fledged, IoC and Eloquent enabled framework.