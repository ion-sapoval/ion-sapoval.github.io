---
layout: default
title:  "Build hybrid applications with AppBuilder(former Icenium)"
date:   2014-05-13
categories: hybrid applications cordova appbuilder
---

# Build hybrid applications with AppBuilder(former Icenium)

I'm not a mobile applications developer, but inevitably from time to time I have to develop some mobile components of the products I'm working on, usually these are not complex mobile applications, however I should learn Android platform, IOS platform, Windows phone and so on, and frankly I don't see this happening. Being a web developer I decided to try the hybrid mobile applications path, which permits me to develop everything by using html with JavaScript and as a final result I will have a perfectly valid native mobile application. There're several hybrid applications development platforms, but in my case I chose Apache Cordova, which is a mature and very well documented platform with a nice JavaScript api which permits to have one code base for all important mobile platforms for which you're developing your application, you can find more details [here](http://cordova.apache.org/docs/en/3.0.0/guide_overview_index.md.html#Overview). Basically Cordova is wrapping your html and JavaScript in a native container app specific for each mobile platform, this container contains 2 main components:

1.	A control which permits to render html and run JavaScript, basically a browser container
2.	A bridge between JavaScript api and device's operating system

With Cordova everything is very nice till the moment you want to generate builds for different platforms, unfortunately for being able to use a window phone emulator or to create a build for windows phone platform we should have a windows os with windows phone sdk installed, alike is with IOS you should run your build process on a mac and so on. Plus the main method of working with Cordova is through Command Line Interface which is not the most comfortable way to do things, not to mention Cordova installation and configuration process not one of the easiest things to do. But all these issues are solved by Telerik's AppBuilder platform which provides a very nice set of tools for building hybrid apps based on Corodova. Main advantage of the AppBuilder is that it provides a unified way for building apps for Android,IOS and WP by removing the necessity to have separate operating systems and  development environments for each platform. How they do it, by making builds in the cloud. AppBuilder provides 3 different IDEs (MIST-online IDE, GRAPHITE and Visual Studio extension) with debugging capabilities and a custom device simulator. There're many other useful things like updating application directly from cloud with a new version, or you can run it inside an AppBuilder container which doesn't require a development certificate for IOS, you have also a nice integration with Everlive services, which is a cloud platform from Telerik and many, many other things which you can find on their [site](http://www.telerik.com/appbuilder). Of course there're some drawbacks from making builds in cloud like: it is a time consuming process and it requires an active internet connection but all these can be overlooked when we think of all the advantages we gain by using AppBuilder.


<script>
var disqus_config = function () {
this.page.url = hybrid-apps-appbuilder;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = hybrid-apps-appbuilder; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>