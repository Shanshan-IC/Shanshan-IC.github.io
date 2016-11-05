---
layout: post
title: Indeed Tokyo Online Test 2017 cn2016fall3
category: Interview
tag: [Interview, C++]
---

Codes for Indeed Tokyo 2017 Online Test, but I forgot the questions, only update the submission.

Question A: Calculate Sequence

{% highlight java %}
#include <iostream>
 
using namespace std;
 
int getSequence(int a, int b) {
    int t = 1;
    for (int n=3; n<=10; n++) {
        t = b;
        b = b+a;
        a = t;
    }
    return b;
}
 
int main() {
    int a, b;
    while (cin >> a>> b)
        cout << getSequence(a, b) << endl;
    return 0;
}
{% endhighlight %}

Question C: Anagram Multiple Number

{% highlight java %}
#include <iostream>
#include <string>
#include <unordered_map>
using namespace std;
 
bool isSame(int n, int m) {
    unordered_map<int, int> map;
    while (n>0) {
        int k = n%10;
        map[k]++;
        n = n/10;
    }
    
    while (m>0) {
        int b = m%10;
        if (map[b]==0)	return false;
        map[b]--;
        m = m/10;
    }
    return true;
}
 
int getCount(int n) {
    int count = 0;
    int len = to_string(n).size();
    
    // substract
    for (int i=2; i<10; i++) {
        int temp = n / i;
        if (n % i !=0)	continue;
        else {
            if (to_string(temp).size() < len)
                break;
            else
                if (isSame(temp, n))
                    count++;
        }
    }
    //multiple
    int i=2;
    for (; i<10; i++) {
        int temp = n * i;
        if (to_string(temp).size() > len)
            break;
        else 
            if (isSame(temp, n))
                count++;
    }
    return count;
}
 
int main() {
    int n;
    while (cin >> n)
        cout << getCount(n) << endl;
    return 0;
}

{% endhighlight %}

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
