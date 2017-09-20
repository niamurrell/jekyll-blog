---
layout:     post
title:      Virtual Types
author:     Nia
tags: 		  MongoDB Mongoose Testing
subtitle:  	Daily Review
category:   daily
---

Learned another thing that directly applies to my app which is great--**virtual types** are what you use to store information on your server as a result of the data that's stored in your database. For example, in my [Value App](https://niamurrell.github.io/search/#ValueApp) I need a constantly-updated count of the number of times the user has used a `thing` in order to calculate its current value. Before learning about virtual types, I thought I would be calling `thingArray.length` all the time, or would have to manually increment a `usageCount` variable each time there was a new use. Not so! I just need to set a virual type to count however many usages are present whenever it's time to do the calculation. This following code shows how to set it up. This is declared outside of the model.
```javascript
UserSchema.virtual("usageCount").get(function() {
  return this.things.length;
});
```

And this is how you can write a Mocha test for it:
```javascript
const assert = require("assert");
const User = require("../src/user");

describe("Virtual Types:", () => {
  it("usageCount returns number of usages", (done) => {
    const joe = new User({
      name: "Joe",
      things: [{ title: "ThingTitle" }]
    });

    joe.save()
      .then(() => User.findOne({ name: "Joe" }))
      .then((user) => {
        assert(joe.things === 1);
        done();
      });
  });
});

```

### Up Next

Debating whether to go to a meetup tomorrow where I might be able to get some help on my [double login problem](https://niamurrell.github.io/daily/2017/09/17/triple-dead-end/).