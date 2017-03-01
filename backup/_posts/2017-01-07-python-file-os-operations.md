---
layout:     post
title:      Python OS File Operations
category:   [Python] 
tags:       [Python]
---

Open the file for writing and reading.

{% highlight Python %}
import os

input = open(filename, 'r')	# read
output = open(filename, 'w') # write
output = open(filename, 'a') # write more
{% endhighlight %}

Walk the whole folder

{% highlight Python %}
for root, dirs, files in os.walk(path, topdown=False):
	#hanlde file
	for name in files:
		if name[:-3] = 'exe':
		print name
{% endhighlight %}

Delete Files

{% highlight Python %}
top='mydata/'
for root,dir,files in os.walk(top,topdown=False):
      for name in files: 
     os.remove(os.path.join(root,name))

os.rmdir('mydata')
os.mkdir('mydata')
{% endhighlight %}
