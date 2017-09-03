---
layout: default
title:  "Apply session state behavior per action in Asp.Net MVC"
date:   2012-02-25
categories: mvc c# asp.net
fileName: 2012-02-25-per-action-custom-sessionstateattribute.markdown
---

# Apply session state behavior per action in Asp.Net MVC

   Last week after I read an interesting article: [Parallel processing of concurrent Ajax requests in Asp.Net MVC](http://www.stefanprodan.eu/2012/02/parallel-processing-of-concurrent-ajax-requests-in-asp-net-mvc)  I created a small mvc project and started to fool around with all kind of combinations between **SessionStateAttribute** and parallel Ajax requests and everything went well, it was exactly the behavior described in the blog article i've mentioned. After that I was curious what is the default behavior regarding session locking when no **SessionStateAttribute** is present and made some tests from which i obtained the  following results: When a new session is created and there was no write operations performed on it, then requests are treated the same as in case of using **SessionStateBehavior.ReadOnly**, but after first write action on the session, all the following request are processed in **SessionStateBehavior.Required** mode which is equivalent with “good bye parallel request execution”,  of course we can to impose a custom session state behavior by applying **SessionStateAttribute** on controller, but that mean that  all actions from that controller will have the same session state behavior which in most cases is not a problem, but what if I have to write and read from a session, and from the same controller I want to execute some actions in parallel which has nothing to do with session, what solutions do I have for this scenario? Of course I can move all my parallel actions into different controller and change it session state behavior, but wouldn’t it be nice if I had an attribute which will permit to change session state behavior per action, and since there is no such attribute in .Net framework by default, I made a custom one.

Next I’ll show you how to create and use this custom attribute.

 

 **1** Create custom attribute class
{% highlight c# %} 
    [AttributeUsage(AttributeTargets.Method, AllowMultiple = false, Inherited = true)]
    public sealed class ActionSessionStateAttribute : Attribute
    {
        public SessionStateBehavior Behavior { get; private set; }

        public ActionSessionStateAttribute(SessionStateBehavior behavior)
        {
            this.Behavior = behavior;
        }
    }
{% endhighlight %}

 **2** Create/Modify custom controller factory
{% highlight c# %} 
public class CustomControllerFactory : DefaultControllerFactory
    {
        protected override SessionStateBehavior GetControllerSessionBehavior(RequestContext requestContext, Type controllerType)
        {
            if (controllerType == null)
            {
                return SessionStateBehavior.Default;
            }

            var actionName = requestContext.RouteData.Values["action"].ToString();
            MethodInfo actionMethodInfo;

            try
            {
                actionMethodInfo = controllerType.GetMethod(actionName, BindingFlags.IgnoreCase | BindingFlags.Public | BindingFlags.Instance);
            }
            catch (AmbiguousMatchException matchExc)
            {
                var httpRequestTypeAttr =
                    requestContext.HttpContext.Request.RequestType.Equals("POST")
                        ? typeof(HttpPostAttribute)
                        : typeof(HttpGetAttribute);

                actionMethodInfo =
                    controllerType.GetMethods().FirstOrDefault(
                        mi =>
                        mi.Name.Equals(actionName, StringComparison.CurrentCultureIgnoreCase) && mi.GetCustomAttributes(httpRequestTypeAttr, false).Length > 0);
            }


            if (actionMethodInfo != null)
            {
                var actionSessionStateAttr = actionMethodInfo.GetCustomAttributes(typeof(ActionSessionStateAttribute), false)
                                 .OfType&ltActionSessionStateAttribute&gt()
                                 .FirstOrDefault();

                if (actionSessionStateAttr != null)
                {
                    return actionSessionStateAttr.Behavior;
                }
            }

            return base.GetControllerSessionBehavior(requestContext, controllerType);

        }
    }
{% endhighlight %}

 **3** Confiugre MVC to use your custom controller factory

In Global.asax you should add the following code:

{% highlight c# %} 
 protected void Application_Start()
        {
            ControllerBuilder.Current.SetControllerFactory(typeof(CustomControllerFactory));
        }

{% endhighlight %}

Example of attribute usage:

{% highlight c# %} 
        [ActionSessionState(SessionStateBehavior.Disabled)]
        public JsonResult Test(int id)
        {
            Thread.Sleep(8000);
            return Json("I've slept 8 sec.");
        }

{% endhighlight %}

You can use **ActionSessionStateAttribute** in combination with the controller attribute **SessionStateAttribute**, in this case **ActionSessionStateAttribute** overrides controller attribute on the actions to which it was applied.
  
<script>
var disqus_config = function () {
this.page.url = per-action-custom-sessionstateattribute;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = per-action-custom-sessionstateattribute; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>