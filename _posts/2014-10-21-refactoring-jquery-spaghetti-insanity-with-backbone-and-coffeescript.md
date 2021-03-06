---
layout: post
title: "Refactoring jQuery Spaghetti With BackboneJS And Coffeescript"
description: ""
category: tech
tags: [jQuery, backbone, coffeescript, tech]
---

# For Whom The Client Polls

<img height="300" width="200" style="float: right;" src=
"{{ site.url }}/assets/hemingway.jpg" />


I'm a fan of what I call the Hemingway approach to development - code drunk, refactor sober. While I don't literally mean [that you need to be intoxicated to write software](http://widgetsandshit.com/teddziuba/2009/02/effective-vices-for-the-it-pro.html), I often find it more effective to write bad code and then improve it, rather than trying to get it perfect the first time. Often times the best design abstractions are obvious once the problem is already solved. 


To demonstrate this, I'm taking a piece of somewhat ugly jQuery I wrote, that I then cleaned up with [BackboneJS](http://backbonejs.org). The Backbone refactors makes the code more [declarative](http://en.wikipedia.org/wiki/Declarative_programming) which makes the code's intent easier to understand and build upon with small, isolated functions. Isolating our code into smaller functions makes unit testing a lot more feasible, which part 2 of this post will demonstrate.

When I first saw Backbone, it all seemed far too abstract for what I was trying to do. I was making AJAX calls and updating DOM elements - why do I need an entire MVC framework? It felt like over-engineering a non-problem.

If you are only making a few AJAX calls and handling a few user events, then a little jQuery in a script file is probably all you need. But since the standards of modern web apps often demand real-time interactivity without page refreshes, your logic can often times grow somewhat complex. Soon enough, you are grepping through your codebase looking for element IDs that handlers are attached to, and you've convinced yourself that nobody else writes unit tests for client-side Javascript either. Backbone adds sanity to this madness and I now consider it an extremely valuable tool, even if I still  suspect other [frameworks](https://angularjs.org) [are](http://knockout.js) [overthinking](http://emberjs.org) [things](http://marionettejs.com/).

The primary purpose of BackboneJS, a relatively small library, is not to add functionality but to add organization. It helps separate the code that manipulates data, the code that manipulates DOM elements and handles their events, and the code that glues it all together with backend services. It also does provide a ton of utility functionality, along with its helper [UnderscoreJS](http://underscorejs.org/). This organization is sorely missing from applications that try to do too much with just jQuery and its plugins.

As an aside, both [Backbone](http://backbonejs.org/docs/backbone.html) and [Underscore](http://underscorejs.org/docs/underscore.html) have their source code annotated with line-by-line explanations, which are great resources if you want to improve your Javascript or figure out *exactly* what that function does.

The following code is a mess, so just skim it for now, because I will break it down into parts when I rewrite it. The goal of the code is to follow the loading progress of a collection of 'League' objects, represented as a JSON list of objects, served up via an AJAX endpoint. We want to render the leagues that are finished loading by passing the objects to a template (using Underscore's _.template() function) and appending the resulting HTML to an existing list element on our page. If any leagues are not finished loading, we show a loading bar, and set a timeout to poll the endpoint again in 5 seconds. 

Assuming our endpoint 'leagues/' returns something like this:
{% highlight json %}
    [
      {"name": "my league", "year": "2014", "loaded": true}, 
      {"name": "my other league", "year": "2014", "loaded": false}
]
{% endhighlight %}

And the HTML on our page starts something like this:
  
{% highlight html %}    
    <html>
    <body>
    <img id="league_loading_gif" src="an_image_url.jpg" style="display:none;"/>
    <ul id="leagues_list"></ul>

    <script type='text/template' id='league_template'>
       <h1><%= name %> </h1>
       <h2><%= year %> </h2>
    </script>
...
{% endhighlight %}

We start with the following code:
{% highlight javascript %}
    <script type='text/javascript'>
      $(document).ready(function () {
        league_template = _.template($("#league_template").html());
        var getLeagues = function() {
          $.ajax("leagues/").done(function (leagues_list) {
            $("#leagues_list").empty();
            if (leagues_list.length == 0) {
              $("#league_loading_gif").hide();
            } else {
              var allLoaded = true;
              for (var i = 0; i < leagues_list.length; i++) {
                var league = leagues_list[i]
                if (!league[i].loaded) {
                  allLoaded = False;
                }
                league_html = league_template(leagues[i]);
                $("#leagues_list").append(league_html);
              }
              if (allLoaded) {
                $("#league_loading_gif").hide();
              } else {
                $("#league_loading_gif").show();
                setTimeout(getLeagues, 5000);
              }
            }
          });
        };
        getLeagues();
      });
    </script>
{% endhighlight %}

<table class="image">
  <caption align="bottom">The conception of the code above.</caption>
  <tr><td>
    <img height="300" width="400" src="{{ site.url }}/assets/noodly.jpg" />
  </td></tr>
</table>


## Coffeescript

I am also going to rewrite the code in Coffeescript. Coffeescript is a Javascript preprocessor that simply cleans up the syntax of Javascript and helps you avoid common mistakes. Did you notice that I used a double-equal sign above?

{% highlight javascript %}
    if (leagues_list.length == 0) {
{% endhighlight %}


Probably not, even though it's always a best practice to use type-safe triple-equals comparisons in Javascript. I also forgot to include 'use strict'. With Coffeescript, I simply don't have to worry about these types of problems. I think the Coffeescript here will be pretty obvious, but if you're confused, you can use [this converter](http://js2coffee.org/).

The most important things to know in order to read the examples below is that we use significant whitespace indentation instead of braces, we use '(x) ->' instead of 'function (x) { ', and '@' is a shorthand for 'this.'. We generally omit parentheses around function calls, unless they are needed for clarity. The last expression of a function is implicitly returned. Finally, I will include a few comments, which will be any thing after a # sign on a line.

One interesting thing to note about Backbone and Coffeescript is that they both have an extends() function that do the exact same thing, which is provide classical inheritance via protoype inheritance. I'll write about this in a future post, but in the  meantime you can read about some of those patterns from Javascript guru [Douglas Crockford](http://www.crockford.com/javascript/inheritance.html).

## Refactoring

### Loading The League Model From The Server

The first thing our Javascript does is request the collection from the server. 
{% highlight javascript %}
     var getLeagues = function() {
       $.ajax("leagues/").done(function (leagues_list) {
          ...
        }
     };
     getLeagues();
{% endhighlight %}    

You can note that I use the .done() method on the [Deferred](http://api.jquery.com/category/deferred-object/) object that ajax() return rather than pass a callback, since Deferred/Promises usually leads to more readable code than callbacks.

Our rewrite of this part of the code looks like this:

{% highlight coffeescript %}

    class League extends Backbone.Model
 
    class Leagues extends Backbone.Collection
      model: League
      url: '/leagues'

    $ -> # short hand for $(document).ready()
      leagues = new Leagues()
      leagues.fetch()
{% endhighlight %}      

Here we've just defined our model and a collection of those models, and then asked to fetch it from the server. The collection will automatically create a new instance of the League model for each object it finds in the JSON list returned, and store the fields of that JSON in the model's attributes. Those attributes should be accessed using get() and set() so that the proper events and validation are called. If you want to get the model's raw JSON back, you can always use toJSON().

### Backbone.sync() - What and Why

 Backbone methods like fetch() and save() which read from or write to a datastore delegate the datastore logic to a function called Backbone.sync(), which can be overriden globally or by-class. By default, though, it will assume your models are syncing with a REST backend via $.ajax(), with a URL structure that looks like

    Get the whole collection: GET  /{collection_url}
    Get a model:        GET  /{collection_url}/{model_id}
    Update a model:       POST   /{collection_url}/{model_id}
    ...

And so on. When creating models in your datastore, it's strongly preferable to make sure they have a unique id field. You can name it 'id' or customize its name using 'idAttribute'. While Backbone will assign it's own id called the 'cid', it will give different one to each instance of a model, and without an id it has no way of knowing that two models returned are the same. 

If we want different URL structure, if we want to preprocess the results, or if we want to validate the results before updating the model, there are several Model/Collection methods to override that can provide that functionality. In this case we are retrieving trusted data in a conventional format and so we can stick with the defaults.

What's great about dispatching to sync() is that it creates an abstraction of how your models interact with their datastore without tying it to a specific implementation. The models and collections only retain the common functionality such as parsing, validating, and other data logic which is independent of your store. So if, for example, I have models and collections calling fetch() and save() all over the codebase, but I decide I want to first check a Browser Local Storage cache before I make an AJAX call, I can implement that logic by overriding a single function - and other Backbone developers will know that sync() overrides are the place to look for that kind of logic.

### Using The League Model To Render Two Dynamic Views

#### The Loading Bar View

The next part of the logic we will refactor is when to show the loading image. In our original code, this logic is spread all over. First we check if there are no elements, in which case we hide it, but then when there are elements, we maintain an allLoaded variable that we track while examining each League object to see if any of them aren't loaded, in which case we set it to false.

{% highlight javascript %}
    if (leagues_list.length == 0) {
      $("#league_loading_gif").hide();
      ...
    } else {
      var allLoaded = true;
      for (var i = 0; i < leagues_list.length; i++) {
        league = leagues_list[i];
        if (!league[i].loaded) {
          allLoaded = False;
        }
        ...
      }
      if (allLoaded) {
        $("#league_loading_gif").hide();
      } else {
        $("#league_loading_gif").show();
        setTimeout(getLeagues, 5000);
      }
    }
{% endhighlight %}    

You can see that the logic is spread out across the entire function and intertwined with unrelated logic. This makes it almost impossible to unit test. The Backbone code is going to be much more declarative and only concern itself with whether to show the loading bar or not, and not mixin our calls to setTimeout or templating.

{% highlight coffeescript %}

    #  define a helper function used below
    isLoaded = (model) ->   
      #  Model attributes should be accessed via get() and set()
      model.get('loaded') 

    class LoadingView extends Backbone.View
      # this element should already exist in the HTML
      el: $("#league_loading_gif")

      initialize: -> 
        @collection.on 'sync', => # Note the 'fat' arrow, see below
          if _.isEmpty @collections.models or _.every @collection.models, isLoaded
            # $@el is shorthand for 'this.$(el)'
            @$el.hide()   
          else
            @$el.show()
    loadingView = new LoadingView {collection: leagues}

{% endhighlight %}

This ends up reading closer to what an English description would look like - whenever we sync the leagues with the datastore, if the collection is empty or every league is loaded, hide the loading bar. Otherwise show it. Each Backbone View is associated with a DOM element represented by its 'el' field, which we can either use jQuery to grab an existing one like we did here, or have Backbone create a new one for us. After that, on the initalization of our View we listen to our collection's sync event. 

We have to use Coffeescript's 'fat' arrow syntax so the 'this' pointer is bound to the View object, and not the Collection object that triggers the event. In plain Javascript we would do something like:

{% highlight javascript %}

    var that = this;
    this.collection.on('sync', function(){
      if(_.isEmpty(that.collections.models) || _.every(that.collections.models)) {
        ....

{% endhighlight %}        

which is exactly the type of awkward kludge I use Coffeescript to avoid.


#### The League Information View
The next thing we want to work on is rewriting the template rendering of the League objects.

{% highlight javascript %}
    $("#leagues_list").empty();
    ...
    for (var i = 0; i < leagues_listlength; i++) {
      var league = leagues_list[i]
      ...
      league_html = league_template(leagues[i]);
      $("#leagues_list").append(league_html);
    }
{% endhighlight %}

That is going to turn into this:

{% highlight coffeescript %}

class LeagueView extends Backbone.View
    tagName: 'li' # let Backbone create a new el us for us with this tag
    template: _.template($("#league_template").html()) 
    initialize: ->
      @listenTo @model 'change', @render
    render: ->
      @$el.html(@template(model))
      # Convention is to always return 'this' at the end of render()
      @        

class LeaguesListView extends Backbone.View
    # This should be a 'ul' element that already exists in the HTML
    el: $("leagues_list") 

    initialize: ->
      @listenTo @collection, 'add', @addOne # listenTo() will ensure 'this' is bound to this View

    addOne: (league) ->
      leagueView = new LeagueView {model: league} # creates a new 'li' element
      @$el.append(leagueView.render().el)     # and adds it to our list
{% endhighlight %}

While it's true the new code is a little longer, we're now expressing ourselves a lot more declaratively rather than procedurally, which makes things easier to wrap your ahead around as the application grows in complexity. The code is also a lot better isolated (no ellipses here) and again, will be easier to test.

We listen to an 'add' event rather than a 'sync' event since we are only going to something different when the collection is returned to us with a League object with an 'id' field we haven't seen before. When we get one, we create a new View (which includes a new DOM element) and append it to our list element.

### Updating The League Data View On Data Changes

Wait, what happens if a League object changes though? Our LeaguesListView isn't listening to those events, but you might notice that the LeagueView itself is. as long as the 'id' of the model stays consistent, the Backbone sync('read') call that fetch() makes also update each of the local models with any models the server returns with the same id. That's why we simply have our LeagueView listening to changes on its own model in order to know whether it needs to re-render itself. Note that we are listening to 'change' events rather than 'sync' events since we only want to re-render on a sync that changes a model's attribute. We could even specify which fields we care about changing by listening specifically to a 'change:field' event, but in this case we care about all of them.

Finally, we need to poll the server if all of the leagues are not finished loading. 

{% highlight javascript %}
    if (allLoaded) {
      ...
    } else {
      ...
      setTimeout(getLeagues, 5000);
    }
{% endhighlight %}

Before, this was mixed up with whether we were displaying the loading bar. Now it's on its own.

{% highlight coffeescript %}
    leagues.on 'sync', ->
      if not (_.isEmpty leagues.models or _.every leagues.models, isLoaded)
        setTimeout leagues.fetch, 5000
{% endhighlight %}

We are trying to hand the models fetch method to setTimeout to call in 5 seconds. This won't *quite* work without one small change. The problem is, not surprisingly, related to the 'this' pointer. Specifically, fetch() is an instance method, so we want to make sure the 'this' pointer is pointing to the instance itself, but we are just grabbing the function from the object without binding it to anything. We can ensure that the function will come with it's 'this' pointer properly bound to the instance by adding an initialize method to the Leagues collection with the useful utility from Underscore, bindAll():

{% highlight coffeescript %}

    class Leagues
      initialize: ->
        _.bindAll @, 'fetch'
{% endhighlight %}        

_.bindall() a list of parameters, the first is an instance of a class ad the rest are method names for the class, and makes sure that whenever you grab the a method from an instance, when it's called, the 'this' pointer will be pointing to the instance and not whatever ends up calling the function. 

### Final Code

Here's our final code put together:

<pre>
{% highlight coffeescript %}
    class League extends Backbone.Model

    class Leagues extends Backbone.Collection
      model: League
      url: '/leagues'
      initialize: ->
        _.bindAll @, 'fetch'


    class LeagueView extends Backbone.View
      tagName: 'li' # let Backbone create a new el us for us with this tag
      template: _.template($("#league_template").html())
      initialize: ->
        @listenTo @model 'change', @render
      render: ->
        @$el.html(@template(model))
        # Convention is to always return 'this' at the end of render()
        @        

    class LeaguesListView extends Backbone.View
      # This should be a 'ul' element that already exists in the HTML
      el: $("#leagues_list") 

      initialize: ->
         # listenTo() will ensure 'this' is bound to this View
        @listenTo @collection, 'add', @addOne
      addOne: (league) ->
        # creates a new 'li' element
        leagueView = new LeagueView {model: league} 
        # and adds it to our list
        @$el.append(leagueView.render().el)     

     class LoadingView extends Backbone.View
        # this element should already exist in the HTML
        el: $("#league_loading_gif") 

        initialize: -> 
          # Note the 'fat' arrow, see below
          @collection.on 'sync', => 
            if _.isEmpty(@collections.models) or _.every(@collection.models, isLoaded)
              # $@el is shorthand for 'this.$(el)'
              @$el.hide()   
            else
              @$el.show()

     $ ->
      leagues = new Leagues()
      loadingView = new LoadingView({collection: leagues})
      listView = new LeaguesListView({collection: leagues})
      leagues.on 'sync', ->
        if not (_.isEmpty leagues.models or _.every leagues.models, isLoaded)
          setTimeout leagues.fetch, 5000
      leagues.fetch()

{% endhighlight %}      
</pre>

While I admit that if you're not used to Backbone and Coffeescript, the above code may be a lot less familiar than the jQuery at the beginning, once I got used to it, I find this style much easier to work with. Also, since Backbone is a very popular library, other developers are more likely to be able to jump onto your project and understand what you are trying to accomplish.

I hope I helped provide some insight into the value of Backbone and Coffeescript by giving you a practical example of using them to refactor a real piece of code. Stay tuned for part 2, where I will discuss using Karma, Jasmine, and RequireJS to properly unit test the code provided here - in a way that would have been impossible with the code we started with. 

> “The world breaks every one and afterward many are strong at the broken places.” 
> -- *Ernest Hemingway, A Farwell To Arms*











