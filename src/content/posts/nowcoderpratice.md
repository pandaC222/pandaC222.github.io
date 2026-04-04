---
【必填】文章标题
title: 牛客竞赛每日一题

【必填】发布日期，格式必须为 YYYY-MM-DD
published: "2026-04-05 01:49:00"

【可选】文章描述，会显示在首页卡片上
description: 如果不太难并且很有意义的题我就会更新（可能

【可选】文章封面图路径
1. 外部图片：http://...
2. 本地图片：/assets/images/xxx.png (放在 public 文件夹下)
image: /assets/home/nowcoder.webp

【可选】文章标签，用英文逗号分隔
tags: [算法,每日一题]

【可选】文章分类
category: 算法

【可选】是否置顶，true 为置顶
pinned: false

【可选】置顶优先级，数字越小越靠前 (0, 1, 2...)
priority: 0

【必填】草稿状态。true 为隐藏，发布时必须改为 false
draft: false
---

# 	2026.4.4树上行走

题目链接：https://www.nowcoder.com/practice/0516ea09ce3540dd9f23fbf6f9ab4754?channelPut=tracker2

知识点：并查集

我们有n个点，注意到，这n个点的权值只能是**0或者1**，进入一个点后，所有与该点不同类型的点都会消失（相连的边也会消失），所以我们要求的就是相同点最大的连通块，在这些连通块中，我们可以选择任意一个点来进入，并查集刚好适用于这道题来寻找连通块，对于一条边权值相同的两个点，我们对其边合并边维护连通块最大值即可，最后遍历如果这个节点的父节点的连通块的大小等于最大值，这个点就可以放入ans数组中。

merge时将size小的往size大的上面合并有利于降低树高。
merge时顺便把max_size记录下来，可省去遍历。
ans本来就是从小到大的，不需要重排序。 

代码如下：

~~~cpp
#include<bits/stdc++.h>
#include <vector>
using namespace std;
#define int long long
#define ld long double
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;
const int N = 2e5+10;
int fa[N],sz[N];
int mx;
void init(){
    for(int i = 1; i < N; i++){
        fa[i] = i;
        sz[i] = 1;
    }
}
int find(int x){
    if(fa[x] == x) return x;
    return fa[x] = find(fa[x]);
}
void merge(int x,int y){
    int fx = find(x),fy = find(y);
    if(fx != fy){
        if(sz[fx] >= sz[fy]){
            fa[fy] = fx;
            sz[fx] += sz[fy];
            mx = max(sz[fx],mx);
        }
        else{
            fa[fx] = fy;
            sz[fy] += sz[fx];
            mx = max(sz[fy],mx);
        }
    }
}
void solve(){
    init();
    int n;cin>>n;
    vector<int> a(n+1);
    for(int i = 1;i <= n; i ++) cin>>a[i];
    for(int i = 1;i <= n-1; i ++){
        int u,v;cin>>u>>v;
        if(a[u] == a[v]){
            merge(u,v);
        }
    }
    
    vector<int> ans;
    for(int i = 1; i <=n ; i ++){
        if(sz[find(i)] == mx) ans.push_back(i);
    }
    cout<<ans.size()<<"\n";
    for(auto i : ans) cout<<i<<" ";
}
signed main(){
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(nullptr);
    int t = 1;
    // cin>>t;
    while(t--){
        solve();
    }return 0;
}
~~~

