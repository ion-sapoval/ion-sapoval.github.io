---
layout: default
title:  "LINQ dynamic queries"
date:   2012-11-17
categories: .net c#
---

# LINQ dynamic queries

“Dynamic filters” does this sound familiar to you, I’m pretty sure it does. In my case I had an application which was using EF5 and which had to be able to filter entities based on user selected filters. Filters were provided to the server as a list of pairs (Entity’s PropertyName, FilterValue) and additionally to this was provided a flag which indicated if filters should be joined by using a conjunction or a disjunction. Basically I had to generate dynamically a predicate which would be used in the where part of a Linq query. With a little inspiration from the [How to: Use Expression Trees to Build Dynamic Queries](http://msdn.microsoft.com/en-us/library/bb882637.aspx) I’ve created a helper class which solved my problem. Below you can find the helper class code:
{% highlight c# %} 
public class DynamicLinqHelper&ltT&gt
    {
        //All expressions, from the same predicate, which have to use entity parameter
        //should share the same(same instance) ParamExpression for avoiding bound Exceptions
        private ParameterExpression _paramExpression;

        /// &ltsummary&gt
        /// Creates an expression which corresponds to the
        /// given filter.
        /// &lt/summary&gt
        /// &ltparam name="propertyName"&gtName of the property used in filter&lt/param&gt
        /// &ltparam name="propertyFilterValue"&gtValue to be compared with the value from the entity property&lt/param&gt
        /// &ltreturns&gt&lt/returns&gt
        private Expression CreateEqualityExpression(string propertyName, string propertyFilterValue)
        {
            //Get property by name from the filtered entity type
            var propInfo = typeof(T).GetProperty(propertyName);

            //convert filter value to the type of the property to be compared to
            var convertedFilterValue = Convert.ChangeType(propertyFilterValue, propInfo.PropertyType);

            //Expression which corresponds to the accessing property value
            var fieldExpression = Expression.Property(_paramExpression, propInfo);

            //Expression which corresponds to the filter value
            var constantExpression = Expression.Constant(convertedFilterValue, propInfo.PropertyType);

            //for string filters we want the equivalent of the t-sql " LIKE '%value%' " which is String.Contains method
            if (propInfo.PropertyType.Name.Equals("String"))
            {
                //Expression which corresponds to the call of the Contains method on the string property
                var callExpression = Expression.Call(fieldExpression, typeof(string).GetMethod("Contains"), constantExpression);
                
                return callExpression;
            }

            return Expression.Equal(fieldExpression, constantExpression);
        }

        /// &ltsummary&gt
        /// Creates an Expression for each filter and merges them by using
        /// a conjunction or disjunction logic.
        /// &lt/summary&gt
        /// &ltparam name="propertyWithFilterValues"&gtList of filters (PropertyName,FilterValue)&lt/param&gt
        /// &ltparam name="useConjunction"&gtIndicates how will be filters merged&lt/param&gt
        /// &ltreturns&gt&lt/returns&gt
        public Expression&ltFunc&ltT, bool&gt&gt CreateFilterPredicate(List&ltKeyValuePair&ltstring, string&gt&gt propertyWithFilterValues, bool useConjunction = true)
        {
            Expression whereCondition = null;
            _paramExpression = Expression.Parameter(typeof(T), "entity");

            foreach (var propertyFilterPair in propertyWithFilterValues)
            {
                //creating an expression for the current filter
                var eqExpr = CreateEqualityExpression(propertyFilterPair.Key, propertyFilterPair.Value);

                //merging current expression with the rest of the filter expressions
                whereCondition =
                    whereCondition == null
                        ? eqExpr
                        : (useConjunction
                               ? Expression.And(whereCondition, eqExpr)
                               : Expression.Or(whereCondition, eqExpr));
            }

            return Expression.Lambda&ltFunc&ltT, bool&gt&gt(whereCondition, new[] { _paramExpression });
        }
    }
{% endhighlight %}

And an example of usage you can find below:

{% highlight c# %}
 using (var context = new Context())
            {
                var filters = new List&ltKeyValuePair&ltstring, string&gt&gt 
                                  {
                                      new KeyValuePair&ltstring, string&gt("Id","1"),
                                      new KeyValuePair&ltstring, string&gt("Name","x")
                                  };

                var wherePredicate = new DynamicLinqHelper&ltUser&gt().CreateFilterPredicate(filters,false);

                foreach (var user in context.Users.Where(wherePredicate))
                {
                    Console.WriteLine("id:{0}  name:{1}", user.Id, user.Name);
                }
            }
{% endhighlight %}

I hope that the code from above is self-explanatory and as usual all the necessary exception handling and validations will be added by you.

<script>
var disqus_config = function () {
this.page.url = ef-linq-dynamic-queries;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = ef-linq-dynamic-queries; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
</script>