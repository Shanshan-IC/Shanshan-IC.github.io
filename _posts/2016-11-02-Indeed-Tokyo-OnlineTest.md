---
layout: post
title: Indeed Tokyo Online Test 2017 cn2016fall3
category: Interview
tag: [Interview, C++]
---

Codes for Indeed Tokyo 2017 Online Test, but I forgot the questions, only update the submission.

Question D: Construct Permutation

{% highlight java %}
#include <iostream>
#include <vector>
#include <unordered_map>
 
using namespace std;
 
int dp[105][105];
vector<int> trouble(105, 0);
 
int getMax(int n) {
    int res = trouble[0];
    int index = 0;
    for (int i=1; i<=n; i++)
        if (trouble[i] > res) {
            res = trouble[i];
            index = i;
        }
    trouble[index] = 0;
    return index;
}
void getPerm(int n) {
    vector<int>vec(n+1, 0);
    unordered_map<int, int> map;
    int index = getMax(n);
    for (int i=1; i<105 && index!=0; i++) {
        for (int j=1; j<=n; j++) {
            if (dp[j][index]==0) {
                if (vec[j]!=0)   continue;
                vec[j] = index;
                map[index]++;
                break;
            }
        }
        index = getMax(n);
    }
    int curr = 1;
    for (int k=1; k<=n; k++) {
        if (vec[k]!=0)
            continue;
        while (map[curr]!=0)
            curr++;
        vec[k] = curr++;
    }
 
    for (int i=1; i<=n; i++)
        cout << vec[i] << endl;
}
 
int main() {
    int N, M;
    cin >> N >> M;
    int a, b;
    for (int i=0; i<M; i++) {
        cin >> a >> b;
        dp[a][b] = 1;
        trouble[b] += dp[a][b];
    }
    
    getPerm(N);	
    
    return 0;
}

{% endhighlight %}
