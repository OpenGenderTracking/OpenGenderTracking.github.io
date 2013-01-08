---
layout: post
category : blog
tags : [about, history]
author: J. Nathan Matias
---

{% include JB/setup %}

<div align="center"><a href="http://www.flickr.com/photos/natematias/8330858942/" title="Women's writing in UK Newspapers by rubberpaw, on Flickr"><img src="http://farm9.staticflickr.com/8491/8330858942_1438e48a6f.jpg" width="500" height="333" alt="Women's writing in UK Newspapers"></a></div>

Open Gender Tracker is an upcoming suite of open source tools and APIs that will make it easy for newrooms and media monitors to collect metrics and gain a better understanding of gender diversity in their publications. Through a Knight Foundation Prototype grant, Irene Ros of Bocoup will be collaborating with me to make open source software out of my research on gender and get it into newsrooms ([more history here](/blog/2013/01/04/Getting-Started/)).

Understanding Gender in Online News
--------------------------------
Many news organisations and editors want to share diverse voices with their readers. Editorial sections benefit from a variety of voices; journalists want to find the stories they're missing. News organisations want to represent issues fairly, to foster a healthy public sphere, and attract a diverse readership. 

Most news organisations don't have gender data beyond employment. Groups like <a href="http://theopedproject.wordpress.com/">The Op Ed Project</a>, <a href="http://vidaweb.org/">Vida Women in Literary Arts</a>, the <a href="http://whomakesthenews.org">Global Media Monitoring Project</a> many others conduct infrequent, sampled studies of gender in the media. These studies tend to foster lively debate about gender in the news, but they're usually not detailed or fast enough to provide actionable feedback within the fast news cycles that drive what happens in a paper.

Newspapers themselves have a shrinking influence on who gets heard in society, as they participate in a broader diversity of networked gatekeepers. Andrew Sullivan recently [ended his relationship with The Daily Beast](http://mediadecoder.blogs.nytimes.com/2013/01/04/andrew-sullivan-on-going-back-to-future-as-an-indie-blogger/) to go solo. Anita Sarkeesian [raised $158,000](http://www.kickstarter.com/projects/566429325/tropes-vs-women-in-video-games/posts/245217) to write a series on women and videogames. Within papers, the front page is declining in importance. Content curators, from Maria Popova to Reddit, are driving massive amounts of traffic to individual articles. [Social media may soon pass Google](http://www.currybet.net/cbet_blog/2012/03/guardian-facebook-google-traffic.php) as the top source of traffic for some newsrooms. In many cases, algorithms rather than editors now choose what we see on whatever equivalent of the front page readers experience.

In this crazy online world, it's no longer enough to count bylines. If we want to understand gender representation in our time, we need ways to measure this complex ecosystem of players, going beyond who's writing to understand who's speaking and who's sharing.

Measuring Gender Online
----------------
Over the summer, I worked with Lisa Evans at the Guardian Datablog to [analyze gender across an entire year of UK news](http://www.guardian.co.uk/news/datablog/2012/oct/23/women-media-representation-online-news). We wanted to see if how closely reader's likes and shares on social media matched the percentage of content by men and women in different sections of UK newspapers. While audiences tended to read the news whoever wrote it, we saw substantial differences between men and women's writing in other parts of the paper ([click for our interactive infographic](http://natematias.com/medialab/uknews-gender), and ([click here to read how we did it](http://civic.mit.edu/blog/natematias/data-science-for-gender-equality-monitoring-womens-voices-in-the-news)).

Open Gender Tracker will make this kind of analysis easy and automated. It's a straightforward analytics system that takes in a news API or RSS feed and produces gender data about who's writing, who's being written about, and who's being quoted. It will work for a single article as well as thousands of articles at a time.

Making Sense of Gender Data
----------------------
The data produced by Open Gender Tracker will become useful when combined with other information. Over the next few weeks, we're going to create a regular gender report for the Boston Globe by combining our gender data with some of the Globe's internal reporting. We're also going to plug Open Gender Tracker together with projects like [Amo](http://source.mozillaopennews.org/en-US/code/amo/), which aggregates social media metrics for any URL. I'm especially excited about the possibility of mashing up content gender data with audience gender data to gain insight into how content by and about women is received by news audiences.

Work With Us!
-------------

Would you like to use Open Gender Tracker? Do you have an idea for how your newsroom or organisation can make sense of gender data? Contact Irene ros at irene at bocoup.com
