---
layout:     post
title:      Nearing the Finish Line
author:     Nia
tags: 		  Hexo 
subtitle:  	Daily Review
category:   daily
---

One huge step closer to finishing my new site!

### Accessing Data Files

Since I want to have a portfolio section, I need an easy way to add projects and have Hexo generate them as a single page. Each project would have a name, description, some links, etc....basically it's not as straightforward as a list to just loop through. Thankfully Hexo allows you to create data files (either YAML or JSON) to do just this.

First I created a `_data` directory in the `source` folder (the site's source folder, ***not*** my theme's source folder) and added my projects in the YAML format:

```yaml
- name: valueMax
  description: Maximize the value of your money! Calculate the per-use value of purchases over time.
  tech: Node.js, Express, MongoDB, Semantic UI
  code: https://github.com/niamurrell/value-app
  demo: https://valuemax.herokuapp.com/
  image: 
  visible: true

- name: Rides For Rewards
  description: Demo app for Women Who Code Workshop. Rewards platform for LA Metro users.
  tech: Node.js, Express, PostgreSQL, Bootstrap
  code: https://github.com/CodingForProduct/metro_reward
  demo: https://rides-for-rewards.herokuapp.com/
  image: 
  visible: true
```

It also works if the data file is in the JSON format:

```json
[
  {
    "name": "RGB Guessing Game",
    "description": "How well do you know your RBG color values? Test your skills in this course project.",
    "tech": "HTML5, CSS3, JavaScript",
    "code": "https://github.com/niamurrell/rgb-game",
    "demo": "https://codepen.io/niamurrell/full/xPmLMV/",
    "image": "",
    "visible": true
  },
  {
    "name": "Inspirational Quote Generator",
    "description": "Get inspired by a random quote in this freeCodeCamp demo project.",
    "tech": "HTML5, CSS3, JavaScript, API",
    "code": "https://github.com/niamurrell/fcc-quote-generator",
    "demo": "https://codepen.io/niamurrell/full/evyVgg/",
    "image": "",
    "visible": false
  }
]
```

Then I created a `portfolio.ejs` **layout** within my theme, and a portfolio **page** (with `hexo new page portfolio` in the command line) to make sure it's stored in the site's `source` folder, and not contained inside the theme. The page won't get any content added—all of that will need to go directly into the template—but the page is where the title and subtitle will come from (these are also needed by my `header` partial), and how Hexo will generate a page to link to from the menus.

To display the data, I added a for loop into the portfolio.ejs layout:

```html
<% for (var project in site.data.projects) { %>
	<% if (site.data.projects[project].visible === true) { %>

	<ul>
		<li><%- site.data.projects[project].name %></li>
		<li>Description: <%- site.data.projects[project].description %></li>
		<li>Tech: <%- site.data.projects[project].tech %></li>
		<li><a href="<%- site.data.projects[project].code %>" target="_blank">Code</a></li>
		<li><a href="<%- site.data.projects[project].demo %>" target="_blank">Demo</a></li>
	</ul>

	<hr>


	<% } %>
<% } %>
```

So going forward, all I'll need to do to add a new project to the portfolio is add a new entry in the `projects.yml` file and all of the html will be generated automatically.

### Still To Do

There are still two more big features to implement before pushing the site live: making the tags work, and making a search engine work. Then I'll have the new site equal in functionality to this site I'm using now, although I'll make some improvements so hopefully it'll be just a bit better.

One thing I don't love about Hexo is that by default, it makes the index page a blog page, and you can't move the blog to a different location. I'd like to fix that too eventually.


### Other Stuff

Another improvement—I've added my learning plan to the site! I was keeping it in a Google doc but it was pretty unwieldy...I think I'll have a better time keeping it up to date in this new (public!) format.

### Up Next

I wonder if I can finish tomorrow...!?