---
layout: default
title:  "Impressions of a .Net developer after the first Ruby/ROR experience"
date:   2012-011-05
categories: .net ruby
fileName: 2012-11-05-ruby-experiment.markdown
---

# Impressions of a .Net developer after the first Ruby/ROR experience

  I’m an adept of the “Polyglot programming” and that’s why I decided to explore a little the Ruby language and also to take a closer look to the Ruby On Rails framework. Like any developer which is spending most of his time by using a particular programming language with all its afferent tools, when I’m learning something new, involuntarily, I’m making a comparison between new stuff and their correspondence in my “base” language, in my case it’s C#. My Ruby experience started with the installation of the Ruby environment which went pretty well. After I executed my first lines of Ruby code in the Ruby console, I’ve decided to make a step further and to install an IDE which will give me more flexibility and control over my Ruby projects, so I’ve started to search and I’ve ended with Aptana Studio 3 which is a nice IDE but it cannot be compared with Visual Studio which is far superior in all aspects. I don’t expect from an IDE to solve all my problems, or to have the entire set of tools needed in the development process, but a simple, intuitive and flexible editing interface, with a decent intellisense, with the basic debugging capabilities is a must, and unfortunately I couldn’t find a Ruby IDE which fulfills these basic requests. Every time I’m learning something new, related to the programming, I’m doing this by implementing a small application, which in my opinion is the most efficient way of discovering new things, in my case I’ve chosen to implement, by using ROR framework, a site formed from a few web pages which will show some lists of data and will do some basic CRUD operations on that data. After I succeeded with scaffolding of a ROR project (I had some problems with this too, because of the backward compatibility issues from different versions of ROR framework), I had to configure a mysql database adapter for being able to work with database from my application, and here the real fun started. I didn’t succeed to install and configure a Mysql adapter for a 64 bit mysql db so I installed a 32 bit version and after that I have to move some Mysql dlls from one directory to another, to install some gems, to uninstall others, finally I’ve ended by installing a Postgresql server for which I succeeded to install the adapter without having any problems. After that I’ve decided to add some authorization and authentication to my site so I chose to install Devise gem which provided all the functionalities I needed, but again it wasn’t as smooth as I thought it would be.

  I will skip the rest of the implementation details and will continue with my conclusions about my Ruby/ROR experience:

 - There is an obvious lack of good and complete set of developing tools
 - There are too many backward compatibility issues
 - There is a very big variety of gems, but unfortunately many of them aren’t up to date
 - ROR doesn’t provide a plus to productivity comparing with ASP.NET MVC, I do agree with the fact that many cool features were present in ROR framework and Ruby language much earlier than they appeared in .Net world, but now, every good stuff from Ruby/ROR has an equivalent in .Net.
 - In my opinion .Net has a better organized community, which provides a more consistent information than the Ruby community	

I don’t want to discourage Ruby adaptation with all the negative conclusions from above, it’s more a reasoning about why I, as a .Net developer, wouldn’t migrate to this language with all its afferent frameworks. Of course in this little experiment I didn’t mention the performance or project types we can implement by using each platform because it would be like we compare apples with oranges, I’ve focused on the things for which are suitable both platforms.

<script>
var disqus_config = function () {
this.page.url = 2012-11-05-ruby-experiment;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = 2012-11-05-ruby-experiment; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>