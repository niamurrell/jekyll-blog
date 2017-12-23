---
layout:     post
title:      Hexo & Planning
author:     Nia
tags: 		  Hexo
subtitle:  	Daily Review
category:   daily
---

Today I set about planning what I'm going to be working on in the short term. One of the priorities will be my personal portfolio site. I really like using Jekyll for this blog and want to learn how to do it from scratch and with Node.js instead of Ruby. So I found [Hexo](https://hexo.io/) which is another static site generator...I'm going to use it to launch a site by 31 December. So today I spent some time researching the tool and how it works.

### Hexo Intro

Hexo is a node package which allows you to create and compile static websites. So basically, I'll be able to write super-simple markdown files and then run the code through Hexo, which in turn generates all of the HTML files and links and site structure. Then I can upload this generated bundle of files (in effect, a website) to a web host (or most simply, and AWS S3 bucket), and the site will look great. Basically it takes away the need to hard-code individual pages if the goal is to have a static website (and therefore save on server costs). I think it will work perfectly, because I'll be able to add content much more easily to the site.

### Hexo Command Line

To use this tool, most of the work is done through the **Hexo Command Line Interface** (CLI). Here are some of the basic commands I learned about today:
```
npm install -g hexo-cli // installs the Hexo CLI to access commands below
hexo version (or -v) // checks CLI version
hexo init "projectName" // installs the basic folder structure
hexo server // generates static site and opens localhost port to preview
^C // stops server
hexo server --draft // opens localhost port for preview, with draft content included
hexo new "postTitle" // generates new post markdown file in the _posts folder in source
hexo new draft "postTitle" // generates draft in source _drafts folder
hexo new page "pageTitle" // creates new directory within root, with index markdown file
hexo publish "draftTitle" // moves draft from _drafts to _posts folder
```

Note about the **new** command: you can change the default *new* type in the `config.yml` file...for example just typing `hexo new "postTitle"` could be set to create a new draft rather than a new post, and so on. You can also create new *"scaffolds"*, which are the templates these *new* files will be created as.

### Asset Folders

One interesting new thing to remember is how Hexo stores assets which belong to each post. If you set `post_asset_folder` to `True` in the `config.yml` file, any time you create a new post, it will also create an `assets` folder alongside the new post markdown file. In this folder you can store assets like images, etc. which will add to the content of that particular post.

You can then access these assets with their own syntax. There are additional properties that are accessible with these tags. The [documentation](https://hexo.io/docs/) is quite good too!

### Project Plans

There are quite a few more details which are pretty much all in the docs and/or [this YouTube series](https://www.youtube.com/watch?v=Kt7u5kr_P5o&list=PLLAZ4kZ9dFpOMJR6D25ishrSedvsguVSm), where I got a great introduction. My goal is to combine my existing website theme with the theme of this blog and get something launched in 10 days. I'd also like to port this blog over to that site (though probably not within the 10 days) so that I have less websites in general. So the countdown is on!

### Other Stuff

I also picked up a JS course I started before Thanksgiving. So far it's a lot of review but looking forward to getting into the more advanced topics.

### Up Next

I will finish the JS course by the end of the weekend and will work on my portfolio site for the 10-day deadline.