---
layout: default
title:  "ASP.NET CORE cross-platform adventures"
date:   2016-03-02
categories: asp.net core linux cross-platform
---

# ASP.NET CORE cross-platform adventures

After I’ve finished developing a pet project with ASP.NET CORE and test it successfully on Windows, I’ve decided to host it on a Raspberry PI with Linux on it. 

Having an ARM processor I was forced to use Mono, that means some extra installations, but in the end I’ve managed to install all prerequisites. After all configurations have been finished, with much hope and optimism I’ve tried to access my Linux hosted web site … and of course the result was a Mono exception regarding some cast errors in my database entities. 
After some digging, I found that the problem is caused by datetime2 type of a table column from my database, apparently Mono can’t handle this type, so I changed column type to datetime and everything went smoothly, at least on server side. 

I’m hitting refresh button and see how my main web page is loading, but fate decided it was too easy so, a lot of JavaScript errors popped out because the content of one JavaScript file could not be loaded, strange thing was that exactly the same thing was working perfectly on Windows. Basically the request for loading js file …/product.js on Linux wasn’t working and on Windows was. When trying to figure out what the problem was, I saw that corresponding file for product.js was Product.js (with capital P), but being used with Windows which is a case insensitive OS it didn’t ring a bell right away. 

After an hour of investigation, I learned the hard way that Linux is case sensitive OS and Product.js != product.js != product.JS  etc. After renaming the file to product.js, at last I had my first .net web site running on Linux.

<script>
var disqus_config = function () {
this.page.url = asp-net-core-cross-platform-adventures;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = asp-net-core-cross-platform-adventures; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>