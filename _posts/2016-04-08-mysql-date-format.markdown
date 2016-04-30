---
layout: post
title:  "Mysql date format!"
date:   2016-04-03 15:04:23
categories: mytags update
tags: [mytags]
---
You will create a table like feedback and then add a date filed in mysql . You will format tha date like "2days 5hours 31minutes" ,your query add like this


{% highlight ruby %}
SELECT CONCAT(
FLOOR(HOUR(TIMEDIFF(now(), feed_time)) / 24), ' days ',
MOD(HOUR(TIMEDIFF(now(), feed_time)), 24), ' hours ',
MINUTE(TIMEDIFF(now(), feed_time)), ' minutes') AS dateform 
FROM tbl_feedback 
{% endhighlight %}
