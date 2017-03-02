---
layout: post
title: "DiDi Online Test 2017"
category: Interview
tag: Interview CPP
---
* content
{:toc}
DIDI Interview Questions

## First Question

* 平面上有N个点，怎么样才能找到斜率最大的两个点。

Note: 

step 1: 先对N个点的x排序
step 2: 斜率最大的值为最大的point[i+1], point[i]的斜率

```cpp
#include <iostream>
#include <vector>

using namespace std;
bool compare(pair<int,int> i, pair<int, int>j) {
    return i.first<=j.first;
}
int main() {
    vector<pair<int,int>> vs;
    vs.push_back(make_pair<int, int>(1,2));
    vs.push_back(make_pair<int, int>(6,4));
    vs.push_back(make_pair<int, int>(4,6));
    vs.push_back(make_pair<int, int>(2,11));
    vs.push_back(make_pair<int, int>(3,9));
    
    // code part
    double maxs = (vs[1].second-vs[0].second)*1.0/(vs[1].first-vs[0].first);
    sort(vs.begin(), vs.end(), compare);
    for (int i=1; i<vs.size()-1; i++) {
        double temp =(vs[i+1].second-vs[i].second)*1.0/(vs[i+1].first-vs[i].first);
        if (temp>maxs)  maxs=temp;
    }
    cout << "the max one is " << maxs << endl;
}
```

## Second Question

* 在矩形中找到一块面积最大的区域。