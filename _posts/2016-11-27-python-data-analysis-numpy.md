---
layout:     post
title:      Python For Data Analysis Numpy
category:   [Data Mining] 
tags:		[Python, Data Analysis, Numpy]
---

{% highlight Python %}

import numpy as np
import pylab as plt
import seaborn

seaborn.set()

a = np.array([1, 2, 3])

print a
print a.shape
print a.dtype

b = np.array([[0, 2, 4], [1, 3, 5]])
print b
print b.shape
print b.dtype

np.zeros(5)

np.ones(shape=(3, 4), dtype=np.int32)

# operations
c = b * 0.5
print c
print c.shape
print c.dtype

d = a + c
print d
print d[0]   # print the first row
print d[:, 0]   # print the first column

print d.sum()
print d.mean()
print d.sum(axis = 0)

# reshape and update in-place
e = np.arange(12)
print e
f = e.reshape(3, 4)
print f
# set e from index 5 onwards to 0
e[5:] = 0
print e
# f is changed also, that means f is related with e
print f

# combine arrays
print a
np.concatenate([a, a, a])
print b
print d
# use broadcasting
# np.dstack([a, b, d])
np.hstack([b, d])


# create sample data
# create lines
x = np.linspace(0, 2, 10)
plt.plot(x, 'o-')
plt.show()
# create smaple data and noise
x = np.random.uniform(1, 100, 1000)
y = np.log(x) + np.random.normal(0, .3, 1000)
plt.scatter(x, y)
plt.show()

#  sort and searching
# sort x along the second axis
x = np.array([[1, 4], [3, 1]])
out = np.sort(x, axis = 1)
x.sort(axis = 1)
assert np.array_equal(out, x)
print out
# Sort pairs of surnames and first names and return their indices. (first by surname, then by name).
surnames =    ('Hertz',    'Galilei', 'Hertz')
first_names = ('Heinrich', 'Galileo', 'Gustav')
print np.lexsort((first_names, surnames))
# searching
# get the maximum and minimium value
x = np.random.permutation(10).reshape(2, 5)
print "x = ", x
print "maximum values = ", np.max(x, 1)
print "maximum indices = ", np.argmax(x, 1)
print "minimum values = ", np.min(x, 1)
print "minimum indices = ", np.argmin(x, 1)
print "-------------"
x = np.array([[1,0,2,0,3,0,4,5,6,7,8], [1,0,2,0,3,0,4,5,6,7,8]])[1]
print np.where(x == 0)
print "-------------"

print np.__version__
# specific help
print np.lookfor('linear algebra')
print np.info(np.dot)
{% endhighlight %}

Try it, see the compile results!!!