---
layout: default
title:  "Add custom SOAP headers to your service requests"
date:   2014-07-29
categories: .net c# soap headers
---

# Add custom SOAP headers to your service requests

In .Net adding a service reference is a very simple and intuitive process, but when it comes to adding custom SOAP headers to your request made by using generated proxy, suddenly everything becomes obscure and tricky. Below I'll give you an example of how to add this custom header:

   {% highlight xml %}
<soapenv:Header xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">;
<pfx:info soapenv:actor="http://schemas.xmlsoap.org/soap/actor/next" soapenv:mustUnderstand="0" xmlns:pfx="http://somedomain.com">
<pfx:credentials>
<pfx:username xsi:type="soapenc:string" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">USERNAME</pfx:username>
<pfx:password xsi:type="soapenc:string" xmlns:soapenc="http://schemas.xmlsoap.org/soap/encoding/" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">PASSWORD</pfx:password>
</pfx:credentials>
</pfx:info>
</soapenv:Header>
{% endhighlight %}

And I want the header to look exactly like in the sample, even with the same namespace prefixes. For this I will define a CustomHeader class which will be derived from MessageHeader base class.

{% highlight c# %}

public class CustomHeader : MessageHeader
    {
        private readonly string _user;
        private readonly string _password;

        public CustomHeader(string user, string password)
        {
            _user = user;
            _password = password;
        }

        public override string Name
        {
            get { return "info"; }
        }

        public override string Namespace
        {
            get { return "http://somedomain.com"; }
        }

        public override bool MustUnderstand
        {
            get { return false; }
        }

        //override this method for being able to specify namespace prefix name
        protected override void OnWriteStartHeader(XmlDictionaryWriter writer, MessageVersion messageVersion)
        {
            writer.WriteStartElement("pfx", this.Name, this.Namespace);
            this.WriteHeaderAttributes(writer, messageVersion);
        }

        public override string Actor
        {
            get { return "http://schemas.xmlsoap.org/soap/actor/next"; }
        }

        //this method will be used for adding content to your header
        protected override void OnWriteHeaderContents(XmlDictionaryWriter writer, MessageVersion messageVersion)
        {
            writer.WriteRaw(string.Format(@"<soapenv:Header xmlns:soapenv=""http://schemas.xmlsoap.org/soap/envelope/"">
<pfx:info soapenv:actor=""http://schemas.xmlsoap.org/soap/actor/next"" soapenv:mustUnderstand=""0"" xmlns:pfx=""http://somedomain.com"">
<pfx:credentials>
<pfx:username xsi:type=""soapenc:string"" xmlns:soapenc=""http://schemas.xmlsoap.org/soap/encoding/"" 
xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"">{0}</pfx:username>
<pfx:password xsi:type=""soapenc:string"" xmlns:soapenc=""http://schemas.xmlsoap.org/soap/encoding/"" 
xmlns:xsi=""http://www.w3.org/2001/XMLSchema-instance"">{1}</pfx:password>
</pfx:credentials>
</pfx:info>
</soapenv:Header>
",_user,_password));
        }
    }
{% endhighlight %}

Lets say that "client" is the name of our web service proxy instance, then we have to write the following code for adding our custom header:

{% highlight c# %}
             using (var operationContextScope = new OperationContextScope(client.InnerChannel))
                {
                    OperationContext.Current.OutgoingMessageHeaders.Add(new CustomHeader("User name","Password"));
                    
                    //to this call will be prepended custom header that we instantiated earlier
                    client.TestMethod();
                 }
{% endhighlight %}



<script>
var disqus_config = function () {
this.page.url = create-custom-soap-header;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = create-custom-soap-header; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>