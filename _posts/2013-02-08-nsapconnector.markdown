---
layout: default
title:  "NSAPConnector library"
date:   2013-01-28
categories: .net c# sap
---

# NSAPConnector library

I published yesterday another helper library **NSAPConnector** which you can use for making remote function calls (rfc) to a SAP system. Basically this library wraps existing **SAP .Net Connector 3.0** and exposes the most frequent used functionalities under a different form, let say in a more .Netish style. For example below you can find an usage example of **SAP .Net Connector 3.0**
{% highlight c# %}
            var destination = 
                RfcDestinationManager.GetDestination("DestinationName");

            var repository = destination.Repository;

            var functionReference = repository.CreateFunction("functionName");

            functionReference.SetValue("ParamName","ParamValue");

            functionReference.Invoke(destination);

            var resultTable = functionReference.GetTable("ResultTableName");

            for (var i = 0; i < resultTable.RowCount; i++)
            {
                resultTable.CurrentIndex = i;

                Console.WriteLine(resultTable.CurrentRow.GetString("ColumnName"));
            }
      {% endhighlight %}
	  
as you can see it is not a very intuitive api for a .Net developer comparing to the ADO.Net api style which **NSAPConnector** exposes, below is an usage example of my library:

{% highlight c# %}
            using (var connection = new SapConnection("DestinationName"))
            {
                connection.Open();

                 var command = 
                    new SapCommand("functionName", connection);

                command.Parameters.Add("parameterName","parameterValue");

                DataSet resultDataSet = command.ExecuteDataSet();
            }
			
{% endhighlight %}
        
As usual you can find more details and examples on [Github](https://github.com/ion-sapoval/NSAPConnector) and [Codeplex](https://nsapconnector.codeplex.com/), it is also available as NuGet packages [NSAPConnector x86](https://nuget.org/packages/NSAPConnector_x86/) and [NSAPConnector x64](https://nuget.org/packages/NSAPConnector_x64/).

<script>
var disqus_config = function () {
this.page.url = nsapconnector;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = nsapconnector; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>