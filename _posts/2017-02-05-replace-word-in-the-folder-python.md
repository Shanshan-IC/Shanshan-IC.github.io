---
layout:     post
title:      "Replace Words in the Folder Using Python"
category:   Python 
tags:       Python
---
* content
{:toc}

```
import os

# list files

def listFiles(dirPath):
    fileList = []

    for root, dirs, files in os.walk(dirPath):

        for fileObj in files:
            fileList.append(os.path.join(root, fileObj))

    return fileList


def main():
    fileDir = "/Users/fushanshan/Documents/Shanshan-IC.github.io/_posts"

    fileList = listFiles(fileDir)

    for fileObj in fileList:

        f = open(fileObj, 'r+')

        all_the_lines = f.readlines()

        f.seek(0)

        f.truncate()

        for line in all_the_lines:
            f.write(line.replace('[hihoCoder]', 'hihoCoder'))

        f.close()


if __name__ == '__main__':
    main()
```