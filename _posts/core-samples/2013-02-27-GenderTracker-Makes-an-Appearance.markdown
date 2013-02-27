---
layout: post
category : blog
tags : [about, history]
author: Irene Ros
title: GenderTracker Makes an Appearance
---

{% include JB/setup %}

Things have been busy here at OpenGenderTracker central. We've been working away on the core [genderTracker system](http://github.com/opengendertracking/gendertracker) as well as two separate trial applications with our friends at [Global Voices](http://globalvoicesonline.org) and the [Boston Globe](http://bostonglobe.com/). We will be writing more about these trials in the comming weeks, but we figured it was time to introduce you to the main beast - the GenderTracker server. 

The GenderTracker system is a single server that can be run on your local machine or on a virtual machine in the cloud. It is a ruby application that relies on [redis](redis.io), a very versatile and fast key-value store, to be the messaging layer by which a client can communicate with the server. There are pretty detailed dependency and setup instructions in the [README.md](https://github.com/OpenGenderTracking/GenderTracker/blob/master/README.md), but we wanted to take a minute and talk about how the system works overall.

## The Data

GenderTracker knows of the existance of two types of elements: `Jobs` and `Articles`. 

A `Job` is merely a specific grouping for articles. In your client you can choose to group articles as you see fit and GenderTracker just allows you to process articles under the umbrella of a `job`. A `job` may, for example, be a search query of your own data that returns a subset of articles. That's very similiar to what we're doing with the Boston Globe API.

An `Article` is a specific json format that describes a piece of text content using our pre-defined format. This is the beauty of GenderTracker - you can bring in content from your news organization or any other source as long as you first convert it to our predefined format. An `article` looks like this:

{% highlight json %}
{
  "url": "<Article url>",
  "id": "<Unique ID>",
  "body": "<Body of text>",
  "original_body": "<Body of text as originally captured>",
  "title": "<Article title>",
  "byline": "<Author name>",
  "pub_date": "<Publication Date>"
}
{% endhighlight %}

You're welcome to add your own properties beyond the ones we require too, if it makes sense. GenderTracker will just ignore them.

## The Flow

Once your articles are in the proper form, you can start piping them into GenderTracker to be processed. What do we mean by piping? We'll explain that in a minute. First, lets talk about how one interfaces with GenderTracker in general:

GenderTracker expects your first request to be for a new job. Requesting a new job merely assigns you a custom ID that we know will be unique to the GenderTracker server. You can imagine it having to process hundreds of different jobs and so this way, we can guarantee yours will be uniquely identified.

Once a new job has been allocated for you, you can start sending in your articles for processing. GenderTracker can handle articles by accepting either file paths to those articles (at which point those files need to be readable and writeable on the file system,) or the json structure we defined above. 

<img src ="/assets/images/flow_diagram.png" />

When GenderTracker recieves your article, it does a few things:

* It tokenizes it - it takes the body of the article and splits it into separate words that we will then use to compute various metrics. GenderTracker does not destroy any of the original information you sent in, but it will write new properties.
* It calculates gender balance based on the availale metric types. At present, GenderTracker looks at the byline author gender (by comparing against a baby name dictionary) and the pronoun counts in the article that can be directly associated with one gender or another. While this is a very modest beginning, GenderTracker was built explicitly with the intent of extending the number of metrics we are able to compute with minimal changes to the code. You can see the current Metrics that are implemented [on github](https://github.com/OpenGenderTracking/GenderTracker/tree/master/src/metrics). Which ones would YOU add?!

## The Results

At the end of the day, while GenderTracker computes the various metrics available for you, it doesn't make a call as to whether the article leans one way or the other. We leave it to you to decide whether based on the results, an article is, or isn't, appropriatly balanced for your context.

For every available metric, a score will be produced and appended to the article structure under a `metrics` section like so:

{% highlight json %}
{
  "url": "<Article url>",
  "id": "<Unique ID>",
  "body": "<Body of text>",
  "original_body": "<Body of text as originally captured>",
  "title": "<Article title>",
  "byline": "<Author name>",
  "pub_date": "<Publication Date>"
  ...
  "metrics" : {
    "nameOfMetric" : {
      "result" : "Female|Male|Both|Unknown",
      "otherRelevantParams..." : {}
    }
  }
}
{% endhighlight %}

You can see a sample processed article [here](https://gist.github.com/iros/5048653).

We are very excited to share GenderTracker with the community. We're thinking very hard about how to evaluate the content we recieve as well as how to make it incredibly easy to integrate into existing environments. Stay tuned for a detailed dive into the exciting data and findings from our friends at GlobalVoices.



