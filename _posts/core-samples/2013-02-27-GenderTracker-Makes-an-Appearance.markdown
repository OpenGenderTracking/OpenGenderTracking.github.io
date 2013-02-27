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

A `Job` is merely a specific grouping for articles. In your client you can choose to group articles as you see fit and GenderTracker just allows you to process articles under the umbrella of a `job`.

An `Article` is a specific json format that describes a piece of text using our pre-defined format. This is the beauty of GenderTracker - you can bring in content from your news organization or any other content as long as you first convert it to our easy to form and read format. An article looks like this:

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

Once your articles are in the proper form, you can start piping them into GenderTracker to be processed. What do we mean by piping? We'll explain that in a minute. First, lets talk about how one interfaces with GenderTracker in the abstract:

GenderTracker expects your first request to be for a new job. Requesting a new job merely assigns you a custom ID that we know will be unique to the GenderTracker server. You can imagine it having to process hundreds of different jobs and so this way, we can guarantee yours will be uniquely identified.

Once a new job has been allocated for you, you can start sending in your articles for processing, each with the job id you just recieved specified as a separate parameter. You can choose to send a path to the article or the entire body of the article (the json we talked above before) as a string. If you send in a file path, GenderTracker will just make changes to that file and save it back to the disk. If you send in text, GenderTracker will send you the text back and you will be required to persist it yourself in whatever way makes sense.

When GenderTracker recieves your article, it does a few things:

* It tokenizes it - it takes the body of the article and splits it into separate words that we will then use to compute various metrics.
* It calculates gender balance based on the availale metric types. At present, GenderTracker looks at the byline author gender (by comparing against a baby name dictionary) and the pronoun counts in the article that can be directly associated with one gender or another. While this is a very modest beginning, GenderTracker was built explicitly with the intent of extending the number of metrics we are able to compute with minimal changes to the code. You can see the current Metrics that are implemented [on github](https://github.com/OpenGenderTracking/GenderTracker/tree/master/src/metrics). Which ones would YOU add?!

<img src ="/assets/images/flow_diagram.png" />

## The Guts

So now that you know how it works, how do you make it go? Well, GenderTracker has an API, except instead of it being an HTTP API, it uses redis as a messaging queue. In practice, GenderTracker connects to a redis server (a sample config file for a redis server can be found in the `db` folder) and your client needs to connect to that server as well. When you want to ask something of GenderTracker, you publish it to the redis queue. When you want to recieve messages from GenderTracker (like your new job id, or the processed article,) you subscribe to the right channels.

You can see [an example](https://github.com/OpenGenderTracking/globalvoices/blob/master/process.rb) of this interaction in our GlobalVoices sample client.

In practice, to request a new job id:

`publish new_job, <some_unique_id>`

To recieve your new job id:

`subscribe <some_unique_id>`

To process an article for a job:

`public process_article { job_id: <job_id>, path: path/to/article.json }`

Or:

`public process_article { job_id: <job_id>, article: <your article json> }`

To recieve notification when your article is done:

`subscribe process_article_done`

To get overall progress about how your job is doing, you can always read the key of your job_id to get the number of files that have been processed. Note that regardless of whether the processing succeeded or failed, that counter will be incremented! 

`@redis.get(job_id)`

That is it! Stay tuned for a detailed dive into the exciting data and findings from our friends at GlobalVoices.



