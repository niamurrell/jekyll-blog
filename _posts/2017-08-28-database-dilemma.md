---
layout:     post
title:      Value App - Database Dilemma
author:     Nia
tags: 		  Databases
subtitle:  	Daily Review
category:   daily
---

Following on from [yesterday's post](https://niamurrell.github.io/daily/2017/08/27/new-project/) I have been rethinking my selection of MongoDB for the value app. I think it comes down to having a murky understanding of when to use a SQL database versus NoSQL. Originally I thought MongoDB would work best, and then each user document would look something like the below, containing all of their `things` along with their individual information:

```
userSchema = {
	username,
	password,
	things: [
		thing 1,
		thing 2,
		thing 3
	]
}
```

But when I think about it it's clear that this is really poor design. I want the site to display each `use` of a `thing` so that I can edit or delete one if I want. So then in the sketch above, each `thing` really needs to be an array including all of the usage dates. But then what if two users want to track their uses of the same `thing`? Then it's just a mess of `things` being repeated in different documents and it just doesn't make any sense. I could link the `things` as references, but the little I understand about SQL tables and joins makes me think that this structure should be a lot simpler that what I originally planned.

So clearly I need to learn more about SQL, which I already had next up for learning. But now the question is, do I just build this app poorly now because I want to use it and then rebuild it later, or should I take the time to learn more first before deciding? I'm kind of sick of waiting to build while learning! But I also don't want to build something that I know from the start is made poorly.

Hmmmmmm...

### Up Next

I want to do all the things.