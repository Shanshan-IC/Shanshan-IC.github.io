---
layout:     post
title:      Update all Python Packages in one time
category:   [Python] 
tags:       [Python]
---

{% highlight Python %}
import pip
from subprocess import call

for dist in pip.get_installed_distributions():
    call("pip install --upgrade " + dist.project_name, shell=True)

{% endhighlight %}