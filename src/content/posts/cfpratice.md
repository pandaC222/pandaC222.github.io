---
title: "Codeforces每日一题"
published: 2026-04-07
description: 监督自己每天至少写一道灵茶或者羊蹄（也许
image: /assets/home/codeforce.webp
tags: [Codeforces,每日一题]
category: Codeforces
---

# 2026.4.7 Fedya and Array 

题目链接：https://codeforces.com/contest/1793/problem/B

难度：1100（不是摆烂写水题，太累了

知识点：构造

对于一个环形排列，我们要想根据题意，构造出最短数组且相邻绝对差为1，通过观察我们不难想到，我们可以通过只让x为最大值，y为最小值，形式化的[y,y+1,y+2,.......x-1,x,x-1,...y+1],举个实际例子x为3，y为-3，构造的数组为-3，-2，-1，0，1，2，3，2，1，0，-1，-2，这样构造即可

代码如下（cpp）：

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ld long double
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;

void solve(){
    int x, y;cin>>x>>y;
    cout<<2 * (x - y)<<"\n";
    for(int i = y; i < x; i++) cout<<i<<" ";
    for(int i = x; i > y; i--) cout<<i<<" ";
    cout<<"\n";
}
signed main(){
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(nullptr);
    int t = 1;
    cin>>t;
    while(t--){
        solve();
    }return 0;
}
~~~