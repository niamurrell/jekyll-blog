---
layout:     post
title:      Deploying New Blog Site (!!)
author:     Nia
tags: 		  Hexo AWS JavaScript Deployment
subtitle:  	Daily Review
category:   daily
---

I finished my site! So happy. The biggest hurdle was getting the search to work. Not going to write about that here since I did a [massive step-by-step](https://niamurrell.github.io/daily/2018/01/01/adding-search-engine-to-static-site/) in a separate post. But there is one thing I want to recap...

### Arr.indexOf()

I learned a new array method in the process of getting the search to work. You can use `Array.indexOf()` to determine the first index where an item in an array can be found. For example from the [docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf):

```javascript
var array = [2, 9, 9];
array.indexOf(2);     // 2 is at the 0th index
```

If the search element is not in the array, it returns -1:

```javascript
var array = [2, 9, 9];
array.indexOf(7);     // -1; 7 is not in the array
```

I was able to use this to filter search results from a set of data. I started with two arrays of objects: `data` objects contained all of the fields related to a blog post such as title, path, tags, and the post content; `results` objects were output by the search engine and contained a reference which was set to the blog post's path.

 I needed to create a new array of objects in the same format as `data`, but only with the posts that also came in the search `results`, i.e. an array `matches`. This was accomplished by first creating a new array of *only* the posts' paths, and then using `.filter()` to narrow the data down to match the results. But since I needed *all* of the relevant results to be in the `matches` array, a `for` loop would not work, nor would `.map()`, because each of these would `return` out of the function after the first result. `indexOf()` allowed the filter to work with all of the results items:

 ```javascript
function filter_results(data, results) {
	var resultPaths = results.map(function(result) {
		return result.ref;
	});

	return data.filter(function(obj) {
		return resultPaths.indexOf(obj.path) !== -1;
	});
}
 ```

### Deploying to AWS

I've had a placeholder on my [dev site](https://dev.niamurrell.com) for several months...finally time to get some real content on there! The site is served from an [AWS S3](https://aws.amazon.com/s3/) bucket, so it was as simple as generating the site files (command line: `hexo g` from within site directory) and then uploading them to the bucket. In the bucket properties I changed the Static Website Hosting settings so that the index document would be `index.html` instead of `comingsoon.html`. And voila! The site is up live on the long S3 default URL.

To link it to my own domain name there is still some work to do. In order to take advantage of AWS' free SSL certificates, I'm set up to use [CloudFront](https://aws.amazon.com/cloudfront/) to distribute the site. This is necessary because the certificate can only be attached to an EC2 server instance or a CloudFront distribution;  since it's just a static site (i.e. no server needed) CloudFront is the best option. CloudFront basically cashes the site files every 24 hours and stores them on servers around the world, resulting in super-quick loading no matter where someone visits my site from.

First step ([I'm now acutely aware](https://niamurrell.github.io/daily/2017/08/22/css-grid-aws-config/)) is to update the CloudFront settings to point to the new root file:
* Navigate to this particular distribution in the CloudFront dashboard
* Under the **General** tab clicke **Edit**
* Set the **Default root object** to index.html

Now visiting the domain *https://dev.niamurrell.com* brings up the home page of my new site. Yay! But clicking on any link results in the same *permission denied* error page I was getting back in August...so the index page is available for the public but somehow the other S3 bucket contents aren't. But since they **are** available when I visit the long S3 bucket URL, it must be a permission issue between CloudFront and S3.

Turns out there is a [setting](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html#private-content-creating-oai) to adjust for this; an assumption is made that if you want to set up access to an S3 bucket from CloudFront, you also want to block access directly to those S3 URLs. And there is an adjustment that can be made to do this:
* From the CloudFront dashboard, open the distribution in question.
* Click to **Origins**, select the origin, and then click **Edit**
* Change **Restrict Bucket Access** from 'No' to 'Yes' and some more options will appear on the screen.
* Here you can **Create A New Identity** and automatically grant it access to the S3 bucket.

Now going back to the S3 bucket Permissions and reviewing the Bucket Policy, a new policy appears for the CloudFront distribution:

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "2",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::cloudfront:user/CloudFront Origin Access Identity G11234567890"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::dev.niamurrell.com/*"
        }
    ]
}
```

So we should be all set, except for one little note in the AWS [docs](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html#private-content-granting-permissions-to-oai):
>There might be a brief delay between when you save your changes to Amazon S3 permissions and when the changes take effect. Until the changes take effect, you can get permission-denied errors when you try to access objects in your bucket.

So I [wait a while](https://stackoverflow.com/questions/42251745/aws-cloudfront-access-denied-to-s3-bucket) and hope it works... 😐

### While waiting...

Once I get this working I will need to get the AWS command line working on my computer so that I can update the bucket without logging into the AWS website.

In the meantime, finished transferring over the files from the old blog so that when it's ready, I'm ready!

### Up Next

Going to a JS meetup tomorrow and a study session so should be a productive day.
