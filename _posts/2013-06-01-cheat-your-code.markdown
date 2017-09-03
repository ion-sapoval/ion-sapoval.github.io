---
layout: default
title:  "“Cheat” your code as often as you can"
date:   2013-06-01
categories: .net c# opensource
---

# “Cheat” your code as often as you can

   From time to time I’m trying to take a look over some source code from open source projects guided by curiosity or by trying to understand some unclear things regarding that particular project. Everyone knows that scanning code created by others is a good practice, especially if it is a good quality code on which are based projects which are used on a large scale in production environments. For example yesterday I was looking over some **SignalR** source code and beside the fact that I solved my problem regarding some misunderstandings, I discovered some new stuff (at least for me) like  [volatile](http://msdn.microsoft.com/en-us/library/x13ttww7%28v=vs.71%29.aspx) and [checked](http://msdn.microsoft.com/en-us/library/74b4xzyw.aspx) C# keywords, or when should we pay attention to object allocation regarding small object heap and large object heap. I've seen other approaches to the problems which I've encounter in the past and in generally another way of doing and organizing things. Accidentally I discovered a small coding bug which I will report today, in this way I will make a small contribution to the project quality, and the list of benefits can go on and on.

   Basically the idea I’m trying to emphasize is: if you want to become a better programmer, you should take a break from your code and spend some time (to cheat) with code created by others. 

<script>
var disqus_config = function () {
this.page.url = cheat-your-code;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = cheat-your-code; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>