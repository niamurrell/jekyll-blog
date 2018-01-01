---
layout:     post
title:      Adding A Search Engine to A Static Site
author:     Nia
tags: 		  Hexo Lunr Libraries
subtitle:  	Daily Review
category:   daily
---

I have been working on getting a search engine implemented on my new [Hexo](https://hexo.io/)-generated static website. It's been a mission to say the least! Since I'm moving my site from the Jekyll generator to Hexo, I have  a working example of what the end goal is. Here are the steps I took to translate the search function from Jekyll to Hexo, and what ultimately led to success.

> Note: This walk-through assumes you already have a Hexo site set up and access to it from the command line. If that's not the case, check out the [Hexo docs](https://hexo.io/docs/), [this intro to Hexo video series](https://www.youtube.com/watch?v=Kt7u5kr_P5o&list=PLLAZ4kZ9dFpOMJR6D25ishrSedvsguVSm), or [my other Hexo posts](https://niamurrell.github.io/search/#Hexo) for more info about setting up a Hexo site.

### Generating Search Data

This is the necessary first step for searching a static site. After all, we need something to search! For a static site, search data can be stored as a JSON file which contains documents for all of the content on your site. For example:

```json
[
  {"title":"Workshop Day & Major App Work to Do",
    "path":"blog/2017-07-16-workshop-day/",
    "content": "This is the long long long post content that I wrote on my blog. ...",
    "tags": ["array", "of", "tags"],
    "categories": ["array", "of", "categories"]},
  {"title":"RESTful Routing",
    "path":"blog/2017-07-15-restful/"},
  {"title":"Jekyll Blog Success & More Express",
    "path":"blog/2017-07-03-jekyll-blog-success-more-express/"},
  {"title":"Jumping Into the Backend",
    "path":"blog/2017-07-02-jumping-into-the-backend/"},
  {"title":"And So It Begins",
    "path":"blog/2017-07-01-dev-blog-begins/"}
]
```

In real life all of these JSON documents would also contain fields for the post content, any tags or categories, etc, like in the first index. You get the idea!

Jekyll uses [Liquid](http://shopify.github.io/liquid/) as a templating engine, and Jekyll will parse Liquid tags to create a JSON file containing all of this post data. But Hexo doesn't have the same functionality with its templating engine (EJS), so we'll need to generate the JSON in some other way.

Thankfully there are some Hexo plugins built to do just this. First I tried `hexo-generator-search` ([link](https://github.com/PaicHyperionDev/hexo-generator-search)) but found that this plugin is optimized for outputting XML data; although it *can* make a JSON file, the output wasn't clean and had lots of new line `\n` tags and other code remnants in the text. I also tried `hexo-generator-json-content` ([link(https://github.com/alexbruno/hexo-generator-json-content)]) which seemed more promising: it's more customizable as far as which fields are included in the JSON file, and the miscellaneous characters occurred less frequently.

To install this plugin, navigate to your site's directory in the command line and install the plugin with npm:

```
npm i --save hexo-generator-json-content
```

Add your personal configuration to your site's `_config.yml` file (more on this below, or in the [documentation](https://github.com/alexbruno/hexo-generator-json-content)), and the next time you run `hexo generate` or `hexo server`, a new file called `content.json` will appear in your site's root folder.

So now that we've got the data, let's search it!


### Writing A Search Engine

Looking through a lot of Hexo theme repos, it seemed like writing a full search engine is how most of them operate search, if they have it. But since these engines are tied in with each individual theme, it was at times difficult to read through their code and pull apart the pieces that would apply to my own custom theme. I found [this post](http://junonguyen.herokuapp.com/2016/01/22/How-to-create-Local-Search-Engine-for-your-blog-with-hexo-generate-search-plugin/) about how to do it in your own theme which was a start, but it was [this more detailed post with code](http://www.hahack.com/codes/local-search-engine-for-hexo/) that laid it out more clearly (note: the post is in Chinese...thanks Google translate!). Unfortunately as awesome as Google translate is, it also translated some of the code...hah!

Ultimately though, this code kept throwing errors, and in fixing it, I realized that this search engine does way more than I even need. My goal is to generate a list of posts that contain the search term. I won't be displaying the full results or highlighting the search terms or even creating a results page. All of the examples and tutorials I found were doing this, so rather than getting this code to work with my site, I opted to look for something more to the point of what I needed.

### Implementing Lunr

[Lunr](https://lunrjs.com/) is a lightweight JavaScript search engine built to work with static sites. My old Jekyll site uses Lunr to search its JSON file. First I tried basically copying the code from the Jekyll site:

```javascript
jQuery(function () {
	// Initialize lunr with the fields to be searched, plus the boost. This creates an index (idx).
	var idx = lunr(function () {
		this.field("title");
		this.field("url");
		this.field("content", { boost: 10 });
		this.field("tags");
		this.field("categories");
	});

	// Get the generated search_data.json file so lunr.js can search it locally.
	var data = $.getJSON("/search_data.json");

	// Wait for the data to load and add it to lunr
	data.then(function (loaded_data) {
		$.each(loaded_data, function (index, value) {
			idx.add(
				$.extend({ "id": index }, value)
			);
		});
	});

	// Event when the form is submitted
	$("#site-search").submit(function (event) {
		event.preventDefault(); // RTH: per Google, preventDefault() might be the culprit in Firefox
		var query = $("#search-box").val(); // Get the value for the text field
		var results = idx.search(query); // Get lunr to perform a search
		display_search_results(results); // Hand the results off to be displayed
	});

	function display_search_results(results) {
		var $search_results = $("#search-results");

		// Wait for data to load
		data.then(function (loaded_data) {

			// Are there any results?
			if (results.length) {
				$search_results.empty(); // Clear any old results

				// Iterate over the results
				results.forEach(function (result) {
					var item = loaded_data[result.ref];

					// Build a snippet of HTML for this result
					var appendString = '<li><a href="' + item.url + '">' + item.title + '</a></li>';

					// Add the snippet to the collection of results.
					$search_results.append(appendString);
				});
			} else {
				// If there are no results, let the user know.
				$search_results.html('<li>No results found.<br/>Please check spelling, spacing, yada...</li>');
			}
		});
	}
});
```

But this code doesn't work with the Hexo configuration...in fact it doesn't seem to work at all. Turns out Lunr went through a major upgrade, and this code no longer works with the current version of Lunr. So now I get to start from scratch! The [Lunr docs](https://lunrjs.com/docs/lunr.html) are pretty helpful, so I went through it step by step.

#### Step 1: Confirm It's Working At All

Step one was getting anything to show up in the search results. The main change from the code above to the newer version is that the `add` method **must** take place at the same time that the index is being created. I tried it with my JSON file first but it didn't work. So following the documentation, I added a data object directly into the `add` method. I also simplified the result display to see what it actually give back to you:

```javascript
jQuery(function () {
	var idx = lunr(function () {
	this.field('title')
	this.field('body')

		this.add({
			"title": "Twelfth-Night",
			"body": "If music be the food of love, play on: Give me excess of it…",
			"author": "William Shakespeare",
			"id": "1"
		});
	});

	$("#site-search").submit(function (event) {
		event.preventDefault(); /
		var query = $("#search-box").val();
		var results = idx.search(query);
		display_search_results(results);
	});

	function display_search_results(results) {
		var $search_results = $("#search-results");
		var appendString = '<li>' + JSON.stringify(results) + '</li>';
		$search_results.append(appendString);
	}
});
```

This gave the following result...not exactly diamonds, but at least we know it's searching!

```
[{
  "ref": "1",
  "score": 0.40824829046386296,
  "matchData":{
    "metadata": {"love":
    {"body": {}
      }
    }
  }
}]
```

Next I tried adding a second document into the `add` function in order to try more search terms. The result is that it could only search the first document, and would otherwise return an empty array. So let's get that working next...

#### Step 2: Search Multiple Documents

The reason for this is that the `add` method only adds one document at a time. So we need to include a `forEach` function to add each document into the index. We also need to add a `forEach` to the `display_search_results` function to list each result:

```javascript
jQuery(function () {
  var data = [{
    "title": "Twelfth-Night",
    "body": "If music be the food of love, play on: Give me excess of it…",
    "author": "William Shakespeare",
    "id": "1"
    },
    {
      "title": "Romeo and Juliet",
      "body": "Romeo, Romeo, wherefore art thou Romeo? Deny thy father and refuse thy name. Or if thou wilt not be but sworn my love...",
      "author": "William Shakespeare",
      "id": "2"
    }];

	var idx = lunr(function () {
  	this.field('title')
  	this.field('body')

    data.forEach(function (doc) {
      this.add(doc)
    }, this)

	});

	$("#site-search").submit(function (event) {
		event.preventDefault();
		var query = $("#search-box").val();
		var results = idx.search(query);
		display_search_results(results);
	});

	function display_search_results(results) {
		var $search_results = $("#search-results");
    if (results.length) {
      $search_results.empty();

      results.forEach(function (result) {
        var appendString = '<li>' + JSON.stringify(result) + '</li>';
        $search_results.append(appendString);
      });
    } else {
      $search_results.html('<li>No results found.<br/>Please try another search term.</li>');
    }
	}
});
```

Hooray! Now when we search, a result comes up for each document. If the term is in both (like the word *love*), two results are listed. And if we search for a term with no results (like the word *alien*), we are helpfully told as much.

But we're still seeing completely unhelpful results which basically spit back what we searched for. So now lets display something useful!

#### Step 3: Display Useful Results

So Lunr provides search results with a `ref` number, starting at the number 1:

```
[{
  "ref": "1",
  "score": 0.40824829046386296,
  "matchData":{
    "metadata": {"love":
    {"body": {}
      }
    }
  }
}]
```

The data is stored in an array, and these `ref` numbers reflect the position in the array, although it's off by one. So we can create an index variable to link `ref` with the original data, and then call whatever fields we want to display on the page from the data in the `forEach` loop within our `display_search_results` function:

```javascript
results.forEach(function (result) {
  var index = parseInt(result.ref) - 1;
  var item = data[index];
  var appendString = '<li>' + item.title + '</li>';
  $search_results.append(appendString);
});
```

And we have a winner! Now when we search any term within either data item, its title is returned and displayed as a list item in the search results.

#### Step 4: Bringing In External JSON

Now that we know the search engine displays the results we want, let's make the data live outside of this search function. After all, a new JSON file will be generated each time a new post is published to the site, not to mention it will be a pretty large file with new posts being added on a daily basis (sometimes as long as this one!). To start let's use the same simple data but save it to a new file in the root directory of the site; I added a third document for testing purposes:

```json
## /test.JSON
[{"title": "Twelfth-Night",
  "body": "If music be the food of love, play on: Give me excess of it…",
  "author": "William Shakespeare",
  "id": "1"
  },
  {"title": "Taming of the Shrew",
  "body": "Sit by my side, and let the world slip: we shall ne'er be younger.",
  "author": "William Shakespeare",
  "id": "2"
  },
  {"title": "Romeo and Juliet",
  "body": "Romeo, Romeo, wherefore art thou Romeo? Deny thy father and refuse thy name. Or if thou wilt not be but sworn my love...",
  "author": "William Shakespeare",
  "id": "3"}
]
```

The Jekyll site used a jQuery method to load the external JSON file:

```javascript
var data = $.getJSON("/test.json");
```

However when I load this into the current file, it throws an error: `data.forEach is not a function`. By logging the value of `data` I see why: this jQuery method returns an object rather than just the array of data contained in the file; and the `forEach` method only works on arrays, not objects. So we need to find a way to access the array. It's also necessary to recognize that the data may not be fully loaded as soon as the `.getJSON` method is called. This was the result the first time I tried it; the data were loaded, but not in time for the search function to run, and it threw `data is not defined`.

A bit of [stack overflowing](https://stackoverflow.com/questions/23681221/how-retrieve-responsejson-property-of-a-jquery-ajax-object) and [documentation reading](http://api.jquery.com/jquery.getjson/) confirmed that indeed, the `getJSON` method returns a promise to get the JSON, but does not actually complete it at the time the promise is made. Since JavaScript is asynchronous, it keeps processing code (keeping that promise in its back pocket!) and the data isn't actually there when we need it. To get around this we need to be clear that any functions which rely on the data are only called once the data have been fully loaded. So we can put the whole index builder function inside a callback which will only execute once the data have been loaded:

```javascript
var idx;

$.when(
  $.getJSON("/test.json")
).done( function(data) {
  console.log(data);
  idx = lunr(function () {
    this.field('title')
    this.field('body')

    data.forEach(function (doc) {
      this.add(doc)
    }, this)
  });
  console.log(idx);
});
```

Notice that we also take `idx` out and declare it as a global variable; this is to ensure that it's available to the `.search` method that will be run later as part of the search field's event listener. We can confirm that the `data` and `idx` variables are logging the same values as they did when we had the data locally.

But there's still one step to go. We also need to load the data within our `display_search_results` function. We can wrap the existing function components within a similar AJAX callback to achieve the same results:

```javascript
function display_search_results(results) {
  var $search_results = $("#search-results");

  $.when(
    $.getJSON("/test.json")
  ).done( function(data) {

    if (results.length) {
      $search_results.empty();

      results.forEach(function (result) {
        var index = parseInt(result.ref) - 1;
        var item = data[index];
        var appendString = '<li>' + item.title + '</li>';
        $search_results.append(appendString);
      });

    } else {
      $search_results.html('<li>No results found.<br/>Please try another search term.</li>');
    }
  });
}
```

And voila! We have a working search engine accessing data from an external JSON file.

#### Step 5: Searching Blog Data

Now that we know everything is working as it should, it's time to try searching with the JSON file which contains the blog data. If you can recall from waaaay at the beginning of this post, we generated a JSON file using the `hexo-generator-json-content` Hexo plugin. It gives us a format exactly like our test file, but with much much more data. But to start things off, lets start by only searching a few fields. We can turn fields on and off by adding rules to the site's `_config.yml` file:
```yaml
jsonContent:
  meta: false
  keywords: false
  pages: false
  posts:
    title: true
    path: true
    permalink: true
    excerpt: false
    text: false
    categories: false
    tags: false
```

We also need to edit the index builder function to take the new key-value pairs into account:
```javascript
var idx;

$.when(
  $.getJSON("/content.json")
).done( function(data) {
  console.log(data);
    idx = lunr(function () {
      this.ref("path")
      this.field("title")

      data.forEach(function (doc) {
        this.add(doc)
      }, this)
    });
    console.log(idx);
});
```

Notice that we use `this.ref` instead of `this.field` for the path field. This will tell Lunr to treat the post's filepath as the results reference, rather than a random number like we did with the dummy data earlier. Using `path` is ideal because unlike `title` it's guaranteed to be unique; we can use this to build out the links on the results list later too. With this setup, our result output is slightly different than it was before:

```javascript
// result
{"ref": "blog/2017-07-06-terminal-shortcuts/",
"score" :0.5773502691896257,
"matchData":{
  "metadata":{
    "command":{
      "title":{}
      }
    }
  }
}
```

Since we no longer have integers as `ref` values, we can't use the same index lookup that we used with the dummy data. Instead we'll need to pull out any matching documents from the original data, which we can do with the `ref` value and an object filter:

```javascript
function filter_results(data, results) {
	var resultPaths = results.map(function(result) {
		return result.ref;
	});
	return data.filter(function(obj) {
		return resultPaths.indexOf(obj.path) !== -1;
	});
}

var matches = filter_results(data, results);
```

This function has two steps: first we take the `results` (which is an array of objects including our `ref` values) and create a new array which only contains the search results' `path` names. Then we take the `data` array (another array of objects) and filter it by those path names; **[indexOf](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)** is a JavaScript array method which returns `-1` if a search element (the object `path` in this case) doesn't exist in the array. The result is a new array containing only the posts relevant from the search; we store this in the variable `matches`.

We can update our `display_search_results` function to display results based on the `matches` rather than the `results`:

```javascript
function display_search_results(results) {
  var $search_results = $("#search-results");

  $.when($.getJSON("/content.json")).done(
		function(data) {
			var matches = filter_results(data, results);

      if (matches.length) {
        $search_results.empty();

        matches.forEach(function (match) {
          var appendString = '<li><a href="' + match.permalink + '">' + match.title + '</a></li>';
          $search_results.append(appendString);
        });
      } else {
        $search_results.html('<li>No results found.<br/>Please try another search term.</li>');
      }
    }
	);
}
```

I think we all deserve a pat on the back, as we now have a fully operational search engine on our Hexo site 😎.

### Wrapping Up

From here there are a few more customizations to do depending on your individual preferences. For example if you have custom fields in your posts or want to include your tags, categories, etc. you can add them by editing your `_config.yml` file. Don't forget to include these fields in the Lunr `idx` function too! You can also edit `_config.yml` to include pages in your search data, just note that the structure of objects in your `content.json` file will change as a result, and you'll need to account for this in the index builder and `display_search_results` functions. Happy coding!
