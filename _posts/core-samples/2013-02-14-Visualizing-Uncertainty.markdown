---
layout: post
category : blog
tags : [dataviz]
author: J. Nathan Matias
---
{% include JB/setup %}


How can we visualize uncertainty? Adam Hyland's topic today is a great question for this Valentine's Day meeting of the <a href="http://www.meetup.com/bostondatavis/events/100199592/">Boston Dataviz group</a>, organised by <a href="http://twitter.com/ireneros">Irene Ros</a> of Bocoup. Irene opens us up by encouraging us to submit talk ideas to the Boston DataVis Community Talks on March 27th. You can <a href="http://bit.ly/bostonvistalks">submit your talk idea here</a>. She also encourages us to register for the <a href="http://openvisconf.com">OpenVisConf</a>. Merlin Calo invites us to <a href="http://www.meetup.com/html5boston/">HTML5 Boston</a>.

<div align="center"><a href="http://xkcd.com/55/"><img src="http://imgs.xkcd.com/comics/useless.jpg"/></a></div>

Our speaker <a href="http://twitter.com/therealprotonk">Adam Hyland</a> is an economist and software developer based out of Boston. He has been working with R since 2010 and when he isn't writing software, he's also a Wikipedia editor. Adam is also a collaborator of mine, via Bocoup, on <a href="http://opengendertracking.org/">Open Gender Tracker</a>.

We usually do dataviz, Adam reminds us. to carry out a purpose: develop a narrative, inform a decision, or to bring clarity to a problem. The world is a complex place, and we often try to provide clarity. Datavisualisation brings us in contact with that complexity and that clarity.

Adam shows us the Enliven Project's visualization of false rape accusations. What makes it effective? It shows potential number of underreported rapes, the reported rapes, the number of people who faced trial, and the number of people convicted and jailed for rape. When <a href="http://www.slate.com/blogs/xx_factor/2013/01/08/the_enliven_project_s_false_rape_accusations_infographic_great_intentions.html">Slate complained that it was wrong</a>, they defended themselves with what Adam calls a "point estimate." Enliven had looked at the range of reputable estimates, thought about it, and picked a dot in the middle. This was an okay choice, but it wasn't an actual reported datapoint. Enliven had effectively a model to decide the number to pick, and they didn't illustrate the uncertainty in their model at all.

How can we do a better job? Adam assures us that none of us are going to leave satisfied with his answer. One place to start is to ask where people handle uncertainty in visualization. The sciences do it well because they have dealt with statistical methodologies for a century and a half (going back to the <a href="http://www.umass.edu/wsp/statistics/tales/gosset.html">Gosset's work for Guiness</a> or maybe <a href="https://en.wikipedia.org/wiki/Normal_distribution">Gauss</a>). Financial forecasters are also good at this, because their money depends on the quality of the visualisation. 

<div align="center"><iframe width="480" height="360" src="http://www.kickstarter.com/projects/jackadam/dark-sky-hyperlocal-weather-prediction-and-visuali/widget/video.html" frameborder="0"> </iframe></div>

Next, Adam shows us <a href="http://darkskyapp.com/">Dark Sky</a>, an iphone weather forecasting app. Weather is an incredibly difficult thing to predict. The signals we get are noisy-- doppler radar is far from clean-- and the models are far from rock solid. Here's <a href="http://journal.darkskyapp.com/2012/how-dark-sky-calculates-temperature/">how Dark Sky calculates temperature</a>.

We can't rely on scientists to tell us how to visualize uncertainty, Adam tells us, because scientists use highly specialised techniques to convey information to their professional peers. They're little help if we care about communicating with a general audience. Adam shows us an incredibly complicated scientific dashboard and tries to show how confusing it is. He's successful. As my brain melts, I'm tragically stuck in the middle of a row, unable to reach the pizza table for a power-up.

<strong>What is Uncertainty?</strong>
Adam tells us about three kinds of uncertainty. <strong>Stochastic uncertainty</strong> happens when you have an uncontrolled dataset and have to reason about it. <strong>Model uncertainty</strong>, often called model error, occurs when you have reasoning about relationships in your data. You may think that two things are correlated, but a lurking third variable may trip you up. We have the best visual language for the third category, <strong>uncertainty about the future</strong>.

Stochastic uncertainty occurs when we have dispersion in our data, if we're drawing from a sample. Adam shows us an opinion poll from the Milwaukie Journal-Sentinel. The chart shows the margin of error at the bottom of the chart. This is the standard presentation for single opinion polls, and it's incredibly hard to know if the poll supports the conclusion. Even the error margin doesn't include all of the uncertainty within a model.

<div align="center"><a href="http://elections.huffingtonpost.com/pollster/obama-favorable-rating"><img src="http://www.niemanlab.org/images/pollscreenshot.png"/></a></div>

Adam shows us <a href="http://www.niemanlab.org/2012/07/huffington-post-puts-polling-power-in-the-hands-of-developers-with-new-api/">the Huffington Post Pollster API</a>, which shows a regression line across a large number of opinion polls. By showing the individual datapoints, HuffPo shows us the dispersion in the data. The regression line also helps reader infer estimates. What's bad about it?

Political stats writer <a href="https://twitter.com/fivethirtyeight">Nate Silver</a> shows uncertainty really well. Nate was an economics student at the University of Chicago who went into consulting and also did analysis of baseball games. Nate blew away everyone else during the 2008 primary and was recently bought by the New York Times. Nate shows the variation over time and from state to state. Nate repeats his models thousands and thousands of times and shows the distribution of possible outcomes across thousands of runs. His technique doesn't give you a confidence interval.

Not all of us have control over the models we're using. How can we think about stochastic uncertainty? Adam starts by showing us <a href="http://en.wikipedia.org/wiki/Box_plot">boxplots</a>, a one-dimensional measurement of the dispersion of data which shows the dispersion of most of the data. By convention, R also shows datapoints which fall outside of the box. Boxplots are especially good because they're mostly distribution agnostic.

<div align="center"><img src="http://upload.wikimedia.org/wikipedia/commons/thumb/1/1a/Boxplot_vs_PDF.svg/500px-Boxplot_vs_PDF.svg.png"></div>

Adam next shows us a <a href="http://en.wikipedia.org/wiki/Violin_plot">violin plot</a>, "two-dimensional <a href="http://en.wikipedia.org/wiki/Kernel_density_estimation">kernel density</a> estimators." If you cut a violin plot in half and lay it on its side, you see the shape of the distribution. 

<div align="center"><img src="http://upload.wikimedia.org/wikipedia/commons/thumb/3/3a/Violin_plot.gif/621px-Violin_plot.gif"/></div>

Adam reflects again on the Huffington Post poll API plot and shows us a boxplot version of the Obama favorability ratings. His version makes the time difference in distribution much clearer.  (sorry, I didn't get a photo)

Does this actually tell us more about uncertainty? The opposite of good statistics isn't no statistics, it's bad statistics, he tells us. When making estimations, we should pick and appropriate estimator and be able to show how we do it. 

We might object that we're not modelers. Adam argues that we're always making judgments and shows us <a href="http://en.wikipedia.org/wiki/Anscombe's_quartet">Anscombe's quartet</a>, four datasets that are identical when examined using simple summary statistics: mean, variance, correlation, and linear regression.

<div align="center"><img src="http://upload.wikimedia.org/wikipedia/commons/thumb/e/ec/Anscombe%27s_quartet_3.svg/500px-Anscombe%27s_quartet_3.svg.png"/></div>

If we're not careful when creating data visualizations, Adam tells us, we can end up with very very unhelpful results.

Adam points to a variety of other approaches of visualizing uncertainty: <a href="http://en.wikipedia.org/wiki/Contour_line">contour plots</a> and <a href="http://en.wikipedia.org/wiki/Carpet_plot">rug plots</a>. These techniques, unfortunately, make it very hard to present a clear answer.

<div align="center"><a href="http://www.flickr.com/photos/natematias/8475156054/" title="US Gun Deaths by natematias, on Flickr"><img src="http://farm9.staticflickr.com/8234/8475156054_3b7c327837_n.jpg" width="320" height="134" alt="US Gun Deaths"></a></div>

The tension between clear answers and uncertainty isn't one we can solve tonight. What we can do as designers is try to contribute to the visual language of uncertainty. Adam shows us a visualization of <a href="http://guns.periscopic.com/">US Gun Killings</a>, which tries to line up life expectancy with aggregate data about gun deaths, creating a persona for each datapoint. Is it okay to present fictional personas? Adam thinks this kind of artistic license is acceptable when you're aiming for impact.

<strong>Model Uncertainty</strong>
Adam shows us a chart of the traffic received by a podcast. Then he shows us the messy data used to create that chart. We often think that the "web request" is a single thing, but for something like a podcast, a single request is created from many requests. The line graph is not a good representation of the data that comes in. Adam shows us a graph of "the long tail of multi-part requests."

<div align="center"><img width="400" src="http://i.imgur.com/Nd9ezLHl.jpg"/></div>

<strong>Forecast</strong>
Adam shows us Amanda Cox's remarkable 2010 project on <a href="http://www.nytimes.com/interactive/2010/02/02/us/politics/20100201-budget-porcupine-graphic.html">US Budget Forecasts, Compare with Reality</a>. This is cheating, he says, because none of us has access to a time machine. Nevertheless, it's a great illustration of the challenges of showing forecast confidence.

"Timeseries models of confidence get very complex very quickly and are way beyond my pay grade," Adam tells us. One approach involves showing error bars. Another involves "bootstrapping," running the models many many times and showing all of the outcomes.

When visualising uncertainty, there aren't any easy tricks. Adam wraps up by encouraging us to push the visual language. One way to do that is to use more and more box plots, to can expand public visual literacies of uncertainty. Another way is to continue asking these questions, finding new and creative ways to present uncertainty clearly. Finally, we should talk about it more often-- finding, sharing, critiquing, and praising each others' work.

An <strong>addendum</strong>: in the discussion, Lynn Cherney points us to <a href="http://www.r-bloggers.com/visually-weighted-regression-in-r-a-la-solomon-hsiang/">a beautiful post on  visually-weighted regression on the R-Bloggers site</a>.

<div align="center"><img src="http://www.nicebread.de/WP/wp-content/uploads/2012/08/Bildschirmfoto-2012-08-30-um-10.25.52.jpg"/></div>
