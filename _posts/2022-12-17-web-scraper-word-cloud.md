---
layout: post
title:  "Web Scraper + Text Analysis + Sentiment Analysis"
date:   2022-12-17 23:50:39
categories: tools
---
<br>
<h1>Web Scraper + Text Analysis + Sentiment Analysis</h1>
<h2>Web Scraper</h2>
There are two primary sources of codes (both written in <code>Python</code>): [twitterscraper][twitterscraper] by Ahmet Taspinar and [zhihu_spider][zhihu_spider] by 
Liu Ruoyu. Codes can be downloaded from Github through the links.
<br>
<h2>Text Analysis</h2>
Code in this part is written in <code>R</code>.
<h3>Build Corpus</h3>
{% highlight ruby %}
install.packages("tm")
install.packages("SnowballC")
library("tm")
library("SnowballC")
{% endhighlight %}

<h4>Clean The Corpus</h4>
Several things need to be done before we can run the analysis:
<ul>
<li>Convert all text to lower case</li>
<li>Removes Punctuation</li>
<li>Removes common english words</li>
<li>Transforms to root words</li>
<li>Takes out https (since these are tweets there are a bunch of https)</li>
<li>Takes out spaces left by removing previous misc.</li>
</ul>
Using Tweets as an example example, the code should look like:
{% highlight ruby %}
TweetCorpus <- TweetCorpus %>%
  tm_map(removeNumbers) %>%
  tm_map(removePunctuation) %>%
  tm_map(stripWhitespace)
TweetCorpus <- tm_map(TweetCorpus, content_transformer(tolower))
TweetCorpus <- tm_map(TweetCorpus, removeWords, stopwords("english"))
TweetCorpus <- tm_map(TweetCorpus, stemDocument) 
removeURL <- function (x) gsub('http[[:alnum:]]*','', x)
TweetCorpus <- tm_map(TweetCorpus, content_transformer(removeURL))
TweetCorpus <- tm_map (TweetCorpus, stripWhitespace)
inspect (TweetCorpus[1:5])
{% endhighlight %}

<h4>Make Term Document Matrix</h4>
{% highlight ruby %}
Tweetdm <- TermDocumentMatrix(TweetCorpus)
Tweetdm <- as.matrix(Tweetdm)
Tweetdm[1:10, 1:20]
{% endhighlight %}
See freq of words, then exclude to only words showing more than <code>7</code> times
{% highlight ruby %}
eachword <- rowSums(Tweetdm)
eachword
subofeach <-subset(eachword, eachword>=5)
subofeach
{% endhighlight %}

<h3>Generate a Wordcloud</h3>
<code>R</code> packages:
{% highlight ruby %}
install.packages(wordcloud)
install.packages(RColorBrewer)
library(RColorBrewer)
library(wordcloud)
{% endhighlight %}
<br>
{% highlight ruby %}
TweetCloud <- sort(rowSums(Tweetdm), decreasing=TRUE)
set.seed (123)
wordcloud (words=names(subofeach),
           freq=subofeach,
           max.words=30,
           colors=brewer.pal(8, "Dark2"))
{% endhighlight %}
The other way of making a word cloud is using the code [chartjs-chart-wordcloud][chartjs-chart-wordcloud] by Samuel Gratzl. The code is written in <code>Typescript</code> and <code>Javascript</code>.
![word](/static/projects/WordCloud/wordcloud.png)

<br>
<h2>Sentiment Analysis</h2>
<p>Sentiment analysis is the use of natural language processing, text analysis, computational linguistics, and biometrics to systematically identify, extract, quantify, and study affective states and subjective information.</p>
In <code>R</code>, we can use package <code>syuzhet</code>:
{% highlight ruby %}
install.packages(syuzhet)
library(syuzhet)
scores <- get_nrc_sentiment(Slotkinonly)
head (scores)
{% endhighlight %}
However, there is a good package in <code>Python</code> aviliable on Github. The package is called [pattern][pattern], from Computational Linguistics Research Group.
<br>

[twitterscraper]: https://github.com/taspinar/twitterscraper
[zhihu_spider]: https://github.com/LiuRoy/zhihu_spider
[chartjs-chart-wordcloud]: https://github.com/sgratzl/chartjs-chart-wordcloud
[pattern]: https://github.com/clips/pattern
