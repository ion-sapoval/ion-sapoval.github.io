---
layout: default
title:  "FlightJS - first contact"
date:   2014-11-23
categories: javascript framework twitter
---

# FlightJS - first contact

![FlightJS]({{ site.url }}/assets/img/Flight.png "Flight")

Twitter developers made available to community another interesting JavaScript framework which has a great potential: “FlightJS”. This is Twitter’s team description of the product: “*Flight is a lightweight, component-based JavaScript framework that maps behavior to DOM nodes*”.
I decided to take a closer look to this framework because of:

 1. Curiosity
 2. It’s based on different philosophy (a cleaner one) than AngularJS, Knockout or other popular MV* frameworks, to be clear, FlightJS isn’t a MV* framework.
 3. Let face it, till now Twitter’s developers released only good stuff to the “market”.

I took a look to the FlightJS documentation but it wasn’t too useful to me, I couldn’t get how it works and how it should be used, but after digging into their mail client demo app, things became more clearer for me and till now I can say the following:

 1. It doesn’t pollute your html markup from views, there’re no custom attributes and so on.
 2. Twitter devs didn’t try to reinvent the wheel, instead they used JQuery as component used by the framework and for dependency control recommends RequireJS
 3. It doesn’t enforce a certain way of structuring your app, this is kind a good but sometimes it can lead to negative results
 4. Separation of concerns is one of the main pillars of the FlightJS, every component you create or use, can communicate with other components only through events which offers the best decoupling mechanism from the architecture point of view
 5. Components contexts are bind to DOM elements which basically permits to control component’s events visibility and accessibility 
 6. With this framework everything  seems so clean and well organized and which is more important everything is easy to test
 7. There’re 2 things that worry me:
  * It is relatively hard to discover connections between views and JavaScript components. For example if you’ll have to fix a bug related to the information from a textbox it will not be trivial to find what components are involved in populating/updating it.
  * For large applications I think the big number of custom events can be a problem, especially in development process.

Next step for me, will be usage of this framework in some small applications and to see it in action, but sincerely, I’m very optimistic about the results.

  
<script>
var disqus_config = function () {
this.page.url = twitter-flightjs;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = twitter-flightjs; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>