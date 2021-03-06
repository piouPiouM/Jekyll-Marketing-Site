---
layout: post
title: Using CloudCannon with Javascript
header: Using CloudCannon with Javascript
category: Tutorials
author: george
---

![A fake slideshow image](/img/blog/slider.png)
A common question that comes up is “How can I use Javascript with CloudCannon?”. As a heavy javascript user, I would ask the same and that’s why we build CloudCannon from the ground up to handle a wide range of sites. 

There is one rule to know when using javascript with the editable class. <strong>The elements with an editable class must not be rendered or tampered with by the javascript. </strong>

###Sliders/Carousels###

CloudCannon allows you to add the editable class to content that is no visible on page load. As long as the content is on the page to start with it should work. 

To demo this I am going to use [unslider](http://unslider.com/). To add the slider we just need a div with all the slides with their own container:

<pre class="prettyprint linenums">
&lt;div class="banner"&gt;
    &lt;ul&gt;
        &lt;li&gt;This is a slide.&lt;/li&gt;
        &lt;li&gt;This is another slide.&lt;/li&gt;
        &lt;li&gt;This is a final slide.&lt;/li&gt;
    &lt;/ul&gt;
&lt;/div&gt;
</pre>

Then all we need to do is include the scripts required and add a single line of JavaScript:

<pre class="prettyprint linenums">
var options = {
    speed: 500,   //  The speed to animate each slide (in milliseconds)
    delay: 3000,  //  The delay between slide animations (in milliseconds)
    dots: true    //  Display dot navigation
};

$('.banner').unslider(options);
</pre>

Hurray, if we test this we see that we have editable content within a slider. One problem though, the library is messing with the inline editing. Every time the arrow keys are pressed the next slide is shown rather than changing  my caret position. That’s Ok, we just need to disable the arrow keys and the autoplay on the site while inside the editor. 


<pre class="prettyprint linenums">
var options = {
    speed: 500,   //  The speed to animate each slide (in milliseconds)
    delay: 3000,  //  The delay between slide animations (in milliseconds)
    dots: true    //  Display dot navigation
};

if (window.inEditorMode) {
    options.keys = false;
    options.delay = false;
}

$('.banner').unslider(options);
</pre>


This will mean that we have got a customisable slider which works well in both the live site and in the client editor. 

###Accordions###

Accordions are another way of showing and hiding related content. They help declutter a screen and are perfect for things like FAQ’s. There is a good tutorial on how to make a simple JQuery accordion on [jacklmoore.com](http://www.jacklmoore.com/notes/jquery-accordion-tutorial/). This will work perfectly just by adding the editable class to any of the content. Amazingly this would even work with the <a href="/docs#repeatable_regions">Repeatable Regions</a> feature.


###That’s all today###

Thanks for reading. Here's [a demo of the slider](http://sliderdemo.cloudvent.net/). Note it's not pretty but would be easy to style. If you want me to go over any other kind of javascript ui modules or somethings unclear feel free to send me a message. To keep up to date on these posts make sure to [follow us on twitter](https://twitter.com/cloudcannonapp).

