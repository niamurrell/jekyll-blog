---
layout:     post
title:      AWS Lambda Functions & Deployment Progress
author:     Nia
tags: 		  AWS
subtitle:  	Daily Review
category:   daily
---

Site is live and deployed!
![PARTY!!!](http://emojis.slackmojis.com/emojis/images/1471045841/799/dancing.gif?1471045841)

Once I figured out how to make AWS CloudFront and S3 work properly together, everything was fine. Mostly...

### Setting S3 Bucket Permissions

In [yesterday's post](https://niamurrell.github.io/daily/2018/01/01/deploying-new-blog-site/) I wrote about updating the S3 bucket policy so that CloudFront and only CloudFront can access and serve the pages from that bucket. Since CloudFront caches the files in the S3 bucket, I thought that it might take some time before I could see the changes take effect in the browser. A [StackOverflow post](https://stackoverflow.com/questions/42251745/aws-cloudfront-access-denied-to-s3-bucket) also suggested this.

But that wasn't the issue at all. From an article I found: ***Objects do not inherit properties from buckets, and object properties must be set independently of the bucket.*** Basically you not only have to update the bucket permissions for CloudFront to gain access, but you also [MUST](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/GettingStarted.html#GettingStartedUploadContent) make every individual file public as well, a fact which was not included on the AWS guides I was reading yesterday. Today once I found this out, I made the files public, and the whole site was available instantly!

### Root Folders & AWS Lambda Functions

...well, sort of. Although each individual file is available, the linking within the site still isn't working. Let's say a person tries to visit `https://dev.niamurrell.com/portfolio`...this would give an access denied error; but if you tack on to the end and try to visit `https://dev.niamurrell.com/portfolio/index.html` then it works fine.

This is because CloudFront works by authenticating each individual request to objects (aka files) stored in the S3 bucket. If someone requests `/portfolio/`, there isn't actually an object there to authenticate, so nothing loads.  This is where AWS Lambda functions come into play. Lambda functions are snippets of code that you can write and integrate into websites or applications. Unlike running a server, this code stays dormant *until exactly when you need it*, so you only pay for the time that the code is actually running. And better still, the first 1 million requests per month are free—after that it goes up to a whopping $0.20 per additional million requests. I think I'm a long way from breaking the bank!

[This AWS Blog post](https://aws.amazon.com/blogs/compute/implementing-default-directory-indexes-in-amazon-s3-backed-amazon-cloudfront-origins-using-lambdaedge/) details how to get it working, although it's a bit out of date. Also one thing it didn't mention: in the Lambda dashboard you **must** be in a region that supports Lambda functions and CloudFront working together (like US East N. Virginia). That one took me some time to figure out.

In any case, I'm still getting some errors so will continue to work on this.

### Other Stuff

I went to a JS.la lunch today which was great! I learned about a bunch of very awesome-sounding groups and events that I look forward to participating in.

### Up Next

Figure out the Lambda function so that this site can be fully operational once and for all.
