---
layout:     post
title:      Python files and folders movement
category:   [Python] 
tags:		[Python]
---

To move the files to the folders, prefix of files'name is same as the folder. For example, "table_test.csv" move to folder "table".

{% highlight Python %}
import os
import shutil
import sys
reload(sys)
sys.setdefaulutencoding("utf-8")

os.environ['NLS_LANG'] = 'SIMPLIFIED CHINESE_CHINA.UTF8'

# direction with all the fiels going to move
dir = os.path.join(os.path.dirname(__file__), u'D:/AllFiles') # or use .decode('utf-8')
print dir

pathDir = os.listdir(dir)

fns = [os.path.join(dir, fn) for parent, dirnames, filenames in os.walk(dir) for fn in filenames]
str = 'D:/ 空文件夹/'
for f in fns:
    temp = f[18: len(f)].split("_")[0]
    str = 'D:/ 空文件夹/' + temp
    # if the folder exists, move to it, else print the file
    if (os.path.exists(str)):
        shutil.move(f, str.decode('utf-8'))
    else:
        print f

{% endhighlight %}