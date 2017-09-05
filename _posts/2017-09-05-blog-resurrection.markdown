---
layout: default
title:  "Blog resurrection"
date:   2017-09-04
categories: blog resurrection
---

Blog resurrection
====================

The time has come! My blog had to be migrated to another platform, due multiple reasons (hosting, obsolete platform, ease of use etc.).  
After a hour of browsing through Internet to see what will be the options, the decision had been made: I will use as a new platform [GitHub Pages](https://pages.github.com) + [Jekyll](https://jekyllrb.com).  
These are the facts that have determined me to make this decision:
 - GitHub Pages provide a seamless integration on the repo level
 - Jekyll is a very versatile static site generator with an included support for blogging (no DB dependencies, support for templates and much more)
 - Out of the box integration between GitHub Pages and Jekyll
 
 Basically publishing a post will involve:
 1. Create a markup file
 2. Push it in the corresponding git repository
 
 That's it! And this is the exact flow I was looking for.  
  But as we all know there should be a catch, and here it is: Jekyll requires Ruby and other gem dependencies which require a Linux machine for being able to run without any problems a preview version of the blog on the local machine. Being a .Net developer it's kinda equivalent with a PC fan and owner which will result in ![linux vs windows]({{ site.url }}/assets/img/linuxVSwindows.png "Linux VS Windows")  
  Fortunately Microsoft implemented Linux Subsystem on Windows which works like a charm. I didn't have any problems with installing all the prerequisites and running development server for Jekyll.

So now I have no excuse for not to blog! 

<script>
var disqus_config = function () {
this.page.url = blog-resurrection;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = blog-resurrection; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>