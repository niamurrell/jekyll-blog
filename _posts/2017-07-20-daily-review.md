---
layout:     post
title:      Learning Pains
author:     Nia
tags: 		  Struggling
subtitle:  	Daily Review
category:   daily
---

Still no success on finishing this login feature. I keep breaking things and then spending ages fixing them; unfortunately none are resulting in a working login! Here's a great example:

### Session Secret

To initialize an Express session (this is how Passport knows who is using the site, and decides which pages they are allowed to view during the session), you tell the app to use the session with defined options: `app.use(session(sessionOptions));`. To set the options I created a `sessionOptions` variable copied directly from the `express-session` docs:
```javascript
var sessionOptions = {
  secret: 'keyboard cat',
  resave: false,
  saveUninitialized: true,
  cookie: { secure: true }
}
```

...only I didn't want to keep the default `secret` and created a new one in my `.env` file, and then referenced that field in the variable:
```javascript
var sessionOptions = {
  secret: 'process.env.SESSION_SECRET',
  resave: false,
  saveUninitialized: true,
  cookie: { secure: true }
}
```

Well, that's what I ***wish*** I had done! I instead wrote `process.env.SESSION_SECRET` (without the single quotes) and it immediately broke the app as soon as I tried to load a page. At one point I changed it back to the default settings, which worked, but surely using exactly 'keyboard cat' couldn't be the only way to make the function work!? This took quite a few attempts with different combinations before it became clear that it just needs to have quotes around the `secret` value, even if it's referencing the environment file.

And this barely got me *slightly* closer to a working login!

### Up Next

I **must** get this working. That's all!
