---
layout:     post
title:      Sloggin' Through The Login
author:     Nia
tags: 		  ENV Node Express
subtitle:  	Daily Review
category:   daily
---

### Environment Files

Got my `.env` files setup for our system. First added the node package `yarn add --dev dotenv`, added `.env` in the `.gitignore` file, and required the package in the `app.js` file: `require('dotenv').config()`. Then created a `.env` file with a list of variables we don't want to store on GitHub:
```
PGHOST=myHostName
PGPORT=0000
PGUSER=myUserName
PGPASSWORD=myPassWord
DB_NAME=myDatabaseName
```

To use the variables I just enter `process.env.DB_NAME` where I would want the database name to show up, and so on. For collaboration with the group, I also created a `.env.default` file which is *not* included in `.gitignore` and shared with my team. They just see the variable names without the secret information, and can use this to create their own `.env` file with the same details I have.

This was especially helpful because one of my teammates' Postgres database is set up on a different port so we were always switching back and forth as we worked. Now we won't need to do that, and can just keep different port numbers in our own `.env` files.

### Validating Form Inputs

I'm using the node package `express-validator` to make sure the form data is clean: 'email' is actually an email address, the two password fields match each other, password is a certain number of characters, that sort of thing. It was fairly straightforward to implement, but I expect there are a lot more validators I'm not aware of so plan to dive deeper into this at some point.

And while I did figure out how to reject invalid entries from the database, I still have to figure out how to get the errors to generate for the user (not just in the console.)

### Hashing Passwords

I also implemented the node package `bcrypt` to secure user passwords as they are saved in the database. Again, I was surprised at how straightforward this implementation was: just needed to wrap my Sequelize 'create user' command within the `bcrypt` function:
``` javascript
bcrypt.hash(password, saltRounds, function(err, hash) {
    var newUser = {first: first, last: last, email: email, password: hash};
    User.create(newUser);
  });
```


### Other Stuff

Added another Terminal shortcut to be able to open files or folders in Sublime: `alias subl="open -a /Applications/Sublime\ Text.app"`. Always love a good shortcut.


### Up Next

More sloggin'.
