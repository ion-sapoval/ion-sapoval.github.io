---
layout: default
title:  "Handle session expiration during ajax requests in an ASP.NET MVC application"
date:   2011-10-08
categories: mvc c# asp.net ajax javascript jquery
fileName: 2011-10-08-session-expiration-ajax-mvc.markdown
---
# Handle session expiration during ajax requests in an ASP.NET MVC application

   I've worked recently on a project which was developed by using ASP.NET MVC 3 and for the authorization/authentication part we've used Forms Authentication. At the controller level we’ve applied some custom filters in which we handled session expiration and unauthorized accesses, in both cases, default behavior was to redirect user to the login page. Everything was fine till we started to encounter session expirations during ajax calls (in our case we were using jQuery ajax api), the results of this session expirations fall into 2 categories:

 1. For requests that were expecting a json result it will result into some javascript exceptions that will leave your application unresponsive.

 2. For requests that were expecting an html response your web application will be “disfigured” by inserting login page html inside a location that had to contain the expected html response.

All this nasty effects are the result of the redirection to the login page in case of the session expiration or of the unauthorized requests. The solution I chose is composed from 2 parts:

* For avoiding automatic redirection for ajax requests I’m checking each response if it has status code 302(redirection) and is a response to an ajax request, if this conditions are met then I’m deleting RedirectLocation value which is enough to prevent redirection. All this logic I’ve put inside Application_EndRequest from Global.asax.<!-- language: c# -->
{% highlight c# %}
protected void Application_EndRequest(object sender, EventArgs e)
    {
      var context = new HttpContextWrapper(Context);<br/>
      if(context.Response.StatusCode == 302 && context.Request.IsAjaxRequest())
      {
        context.Response.RedirectLocation = null;
      }
    }

{% endhighlight %}
* Registered a global ajax error event handler inside main Layout page which is executed every time an exception is thrown by any ajax request from application, inside this handler I’m verifying if the response status is 302, then I’ll apply session expiration logic (in our case, a message is shown to the user and when the message is closed, user is redirected to the login page)
<!-- language: lang-js -->
{% highlight javascript %}
$("#global_divDialogContainer").ajaxError(function (e, xhr, settings) {

        if (xhr.status == 302) {

            //Code for handling expiration
        }

        return true;
    });  
{% endhighlight %}

For the second step you have to assure that your ajax request have the property global set to true (this is the default value) otherwise the global ajaxError event will not be triggered if an ajax call error will occur.

<script>
var disqus_config = function () {
this.page.url = 2011/10/08/session-expiration-ajax-mvc;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = 2011-10-08-session-expiration-ajax-mvc; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>