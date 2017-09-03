---
layout: default
title:  "PostRequestFactory library"
date:   2013-01-28
categories: webrequest http .net
---

# PostRequestFactory library

From time to time every web programmer has to send http request manually from the server side directly from code, usually we have at our disposal framework classes that know how to send and receive http requests and the only thing we should do is to create the request body and eventually add some headers and cookies. The creation of the request body isn't a very difficult job, but it is a time consuming and error prone task. Several weeks ago I had to generate some http request for being able to use an export functionality exposed by a public server and for that, of course, I had to create some web requests that have multipart/form-data content type, but this time I've decided to make a helper library that I will use for generating this kind of request for the future use. As usual I use my personal projects for learning new stuff and to practice things that I didn't used for a long time. Main objectives were:

 - Create a library that will be easy to use and which will cover the most common scenarios.
 - Use GIT as source control.
 - Use GitHub and Codeplex.
 - Create a NuGet package for this library.
 - Use MsTest for unit testing.

At the end of the project I was proud of myself, because I've accomplished all the objectives. 

Regarding impressions about each objective I'll say a few words about each one.

 - Library creation: I think I've done a good job, but the ultimate verdict will give users of this library(hopefully there will be at least one :) ).
 - Git: I like it a lot,of course I didn't use the biggest part of its features, after all this was a tiny project and with only one developer working on it.
 - GitHub/CodePlex: I liked to work with both, but for me, frankly, CodePlex is more intuitive and easier to use.
 - NuGet: It is fantastic, in 2 minutes you can create and publish your package without being a NuGet guru.
 - Unit testing: I realized that in this moment I can consider myself a beginner in unit testing and this is because of the lack of practicing unit testing in Romanian software companies (all of them consider themselves "Agile" companies, to be Agile you should embrace agile practices and what is more important, to adapt them to your needs and particularities).

If you're curious about PostRequestFactory you can take a look at:

 - [GitHub](https://github.com/ion-sapoval/PostRequestFactory)
 - [CodePlex](https://postrequestfactory.codeplex.com/)
 - [NuGet](http://nuget.org/packages/PostRequestFactory/)

 
<script>
var disqus_config = function () {
this.page.url = postrequestfactory;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = postrequestfactory; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>