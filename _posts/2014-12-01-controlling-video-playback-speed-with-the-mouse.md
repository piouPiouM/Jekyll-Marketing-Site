---
layout: post
title: Controlling video playback with the mouse
header: Controlling video playback with the mouse
category: Tutorials
author: mike
---

Until yesterday, my [personal website](http://mikeneumegen.com) was a video of me eating an apple with an 80's porn star moustache. The moustache is long gone so it's time for an update. <a href="https://vimeo.com/50588111"><img src="/img/blog/video-playback/old.png" alt="old mikeneumegen.com page"></a>

I started with a clean slate. There's a three principles I wanted to reflect in my new site:

### Minimalism
I wanted to take minimalism to the extreme where every word, element and pixel had been carefully considered and placed for a purpose. 

### Curiosity
One thing I liked about my previous website is how it provoked curiosity. Who is this guy? Why is he eating an apple? What's going to happen? 

### Interactive
My previous website didn't have any interaction with the visitor. For such a simple website, interaction makes it much more engaging. It's also a way I can mess around with new technology and fuse my creative and engineering brains.

Eventually I came up with the idea of controlling the video playback speed with the mouse. It's an interaction which doesn't require instructions and adheres to the minimalism principle. Visitors will (hopefully) discover the playback speed changing as they move their mouse. The idea for the video just seems like the next logical iteration on an apple eating video...perhaps I just like people watching me eat.

<a href="http://mikeneumegen.com"><img src="/img/blog/video-playback/new.png" alt="new mikeneumegen.com page"></a>

The code for this is actually fairly simple. I have an event listening to the mouse move to adjust the playback speed based on the distance from the mouse to the center of the video. I've also added a maximum playback rate of 3 so it doesn't get too fast. The divison by 300 is a magic number I'm using to get the sensitivity to feel about right.

<pre class="prettyprint linenums large">
$(document).ready(function() {
	document.onmousemove = function(e) {
		$('.videos video').each(function() { 
			this.playbackRate = Math.min(calculateDistance($(this), e.pageX, e.pageY) / 300, 3);
		});
	};
});
</pre>

The calculate distance function is just a bit of pythagoras magic.

<pre class="prettyprint linenums large">
function calculateDistance(elem, mouseX, mouseY) {
	return Math.floor(
		Math.sqrt(
			Math.pow(mouseX - (elem.offset().left + (elem.width() / 2)), 2) + 
			Math.pow(mouseY - (elem.offset().top + (elem.height()/2)), 2)
		)
	);
}
</pre>

For anyone doing a project like this make sure you film it on an empty stomach. Most of the videos took a few takes to get something where I wasn't laughing or chewing with my mouth open. Needless to say, the lemon was by far the worst.

Check out [my website here](http://mikeneumegen.com). I'm really keen to hear anyone's feedback. Is it interesting or are you too grossed out?