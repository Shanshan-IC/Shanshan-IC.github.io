 ---
layout:     post
title:      Python Pandas Handles Big Data
category:   [Python] 
tags:       [Python]
---

Python block for reading the big data and handling it!

{% highlight Python %}
import pandas as pd
import time
import numpy as np

start = time.clock()
reader = pd.read_csv('data.csv', iterator = True, low_memory = False)

loop = True
chunkSize = 5000000
chunks = []
while loop:
  try:
    chunk = reader.get_chunk(chunkSize)
    chunks.append(chunk)
  except StopIteration:
    loop = False
    print "Iteration is stopped."
df = pd.concat(chunks, ignore_index=True)
print time.clock() - start
{% endhighlight %}