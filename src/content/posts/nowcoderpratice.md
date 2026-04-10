---
title: "牛客竞赛每日一题"
published: 2026-04-05T01:49:00+08:00
description: "如果不太难并且很有意义的题我就会更新（可能）"
image: "/assets/home/nowcoder.webp"
tags: ["算法", "每日一题"]
category: "牛客"
pinned: false
priority: 0
draft: false
---
# 	2026.4.4树上行走

题目链接：https://www.nowcoder.com/practice/0516ea09ce3540dd9f23fbf6f9ab4754?channelPut=tracker2

知识点：并查集

我们有n个点，注意到，这n个点的权值只能是**0或者1**，进入一个点后，所有与该点不同类型的点都会消失（相连的边也会消失），所以我们要求的就是相同点最大的连通块，在这些连通块中，我们可以选择任意一个点来进入，并查集刚好适用于这道题来寻找连通块，对于一条边权值相同的两个点，我们对其边合并边维护连通块最大值即可，最后遍历如果这个节点的父节点的连通块的大小等于最大值，这个点就可以放入ans数组中。

merge时将size小的往size大的上面合并有利于降低树高。
merge时顺便把max_size记录下来，可省去遍历。
ans本来就是从小到大的，不需要重排序。 

代码如下（cpp）：

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



# 2026.4.6 **小苯的麦克斯** 

题目链接：https://www.nowcoder.com/practice/de5b60b23a014f1bb66b8164faea3d0d?channelPut=tracker2

知识点：mex

mex: **最小未出现非负整数**

我们需要求选择一个连续区间最大的max-mex值，这个区间最小长度为2，我们由mex的定义知对于一个区间只有0，1，2，3，4这种连续的数才能使mex不短增大，如果区间最小值为1，那mex就是0了，因此我们很容易得到取两个区间时可以使mex最小，因此我们可以在max两边取区间，同时考虑边界情况，如果max=min的情况得特判，如果max=min=0，输出-1;如果最大值为0，也输出-1，其他情况正常判断就行

这样判断写起来好像比较麻烦，其实可以每次取两个区间求它们的max-mex同时用ans维护最大值即可，这样写起来比较简短，我只给出第一种解法

代码如下（py）：

~~~python
import sys
input = sys.stdin.readline
t = int(input())
for _ in range(t):
    n = int(input())
    a = list(map(int,input().split()))
    mx = max(a)
    mn = min(a)
    ans = 0
    if mx == 0:
        print(-1)
        continue
    if mx == 1:
        if mn == 1:
            print(1)
        else:
            print(-1)
        continue
    if a[0] == mx:
        if a[1] == 0:
            ans = max(mx - 1, ans)
        else:
            ans = max(mx, ans)
    if a[-1] == mx:
        if a[-2] == 0:
            ans = max(mx - 1, ans)
        else:
            ans = max(mx, ans)
    for i in range(1,n-1):
        if a[i] == mx:
            mn = min(a[i+1], a[i-1])
            if mn == 0:
                ans = max(mx - 1, ans)
            else:
                ans = max(mx, ans)
    print(ans)
~~~



# 2026.4.7 **计算一年中的第几天** 

题目链接：https://www.nowcoder.com/practice/178aa3dafb144bb8b0445edb5e9b812a?channelPut=tracker2

水题

我们判断是否使闰年，闰年(Y % 4 == 0 && Y % 100 != 0 || Y % 400 == 0)2月天数为29天

代码如下（cpp）：

~~~cpp
#include <bits/stdc++.h>
using namespace std;
int m[13] = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
int main() {
    int Y, M, D, d;
    while (cin>>Y>>M>>D) {
        d = D;
        for (int i = 0; i < M; i++) d += m[i];
        if (Y % 4 == 0 && Y % 100 != 0 || Y % 400 == 0) d += 1;
        cout<<d<<"\n";
    }
    return 0;
}
~~~

# 2026.4.8抽卡

题目链接：https://www.nowcoder.com/practice/cddfb87d552c468d9176e95efffa7b3c?channelPut=tracker2

知识点：概率，快速幂，逆元，费马小定理

题目问如果每个卡池里都单抽一次，能抽到自己想要的卡的概率是多少 ，我们通过推断发现直接算能抽到的概率不好算，因为你直接相乘能抽到的概率相当于取交集，因此我们通过算每个卡池抽不到的概率p相乘，P=（1-p1）*（1-p2）....（1-pn），最终答案就是（1-P），但是我们需要mod1e9+7，由于概率可能是个分数，在处理分数模运算，我们需要求逆元，mod是质数，可以根据费马小定理求得逆元，inv(x) = fastpow(x,mod-2)。

代码如下（cpp）：

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ld long double
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;
const int mod = 1e9 + 7;
int fastpow(int x, int p){
    int ans = 1;
    x %= mod;
    while(p){
        if(p&1) ans = ans * x % mod;
        p >>= 1;
        x = x * x % mod;
    }
    return ans;
}
int inv(int x){
    return fastpow(x, mod - 2);
}
void solve(){
    int n;cin>>n;
    int fenzi = 1, fenmu = 1;
    vector<int> a(n+1),b(n+1);
    for(int i = 1;i <= n; i++) cin>>a[i],fenmu = fenmu * a[i] % mod;
    for(int i = 1;i <= n; i++){
        cin>>b[i];
        fenzi = fenzi * (a[i] - b[i]) % mod;
    }
    if(fenzi == 0) cout<<1;
    else cout<<(1 - fenzi * inv(fenmu) % mod + mod) % mod;
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



# 2026.4.9绿豆蛙的归宿

题目链接：https://www.nowcoder.com/practice/764c0b1b34d24122bd9ae75220e370a3

知识点：动态规划

 本题是一道期望dp模板题，正解是动态规划或者记忆化搜索，但是由于牛客数据较弱，正常写不记忆化搜索的dfs也放过去了，这种写法在洛谷中(题目同名)是会T的。 

 注意到，我们需要求从起点1到N**路径总长度的期望值，**我们正常dfs写法，就是从每次从起点dfs到N，记录路径长度len，记录出边数的乘积sz，使用全概率公式求得这条路径的期望长度res，加到总期望ans中，我们给出这种直接dfs的代码：

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ld long double
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;

void solve(){
    int n,m;cin>>n>>m;
    vector<vector<pair<int,int>>> e(n+1);
    for(int i = 1;i <= m; i++){
        int a,b,c;cin>>a>>b>>c;
        e[a].push_back({b,c});
    }
    ld ans = 0;
    auto dfs = [&](auto dfs,int u,int l,int sz)->void{
        if(u == n){
            ans += l*1.0/sz;
            return;
        }
        for(auto [v,w]:e[u]){
            dfs(dfs,v,l+w,sz*e[u].size());
        }
    };
    dfs(dfs,1,0,1);
    cout<<fixed<<setprecision(2)<<ans;
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

 在牛客中这种写法是可以过的，但是在洛谷中会T两个样例，原因是这种暴力的写法在边数非常大时每次重新dfs一次走过的点，复杂度会爆发式增长。 

 ![img](https://uploadfiles.nowcoder.com/images/20260409/272812068_1775734246035/D2B5CA33BD970F64A6301FA75AE2EB22) 

因此我们可以想到用一个数组f[n]每次记录走过的点的期望，这样再次走这个点u时直接返回f[u],这样的话我们每个点只会遍历1次，每条边也遍历一次，因此复杂度就会来到O(n+m)，这就是记忆化搜索优化时间复杂度，这样我们就可以通过这道题了。

这是一个从后往前的过程，因为我们dfs在走到终点时才往回返回记录f[u]的值，答案就是f[1]，注意到，我们到底已经终点u==n后期望值为0，因为我们已经到底了，直接返回0就行。

便于理解，这里给出样例递归搜索树：

 ![img](https://uploadfiles.nowcoder.com/images/20260409/272812068_1775734595349/D2B5CA33BD970F64A6301FA75AE2EB22) 

 接下来我们给出记忆化搜索写法的代码： 

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ld long double
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;

void solve(){
    int n,m;cin>>n>>m;
    vector<ld> f(n+1,-1);
    vector<vector<pair<int,int>>> e(n+1);
    for(int i = 1;i <= m; i++){
        int a,b,c;cin>>a>>b>>c;
        e[a].push_back({b,c});
    }
    auto dfs = [&](auto dfs,int u)->ld{
        if(u == n) return 0;
        if(f[u] != -1) return f[u];
        ld res = 0;
        for(auto [v,w]:e[u]){
            res += (dfs(dfs,v) + w)*1.0/e[u].size();
        }
        return f[u] = res;
    };
    dfs(dfs,1);
    cout<<fixed<<setprecision(2)<<f[1];
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

 当然，记忆化搜索和dp本质相同，我们通过简单改写就是dp写法了 

 代码如下： 

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ld long double
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;

void solve(){
    int n,m;cin>>n>>m;
    vector<ld> dp(n+1,0);
    vector<vector<pair<int,int>>> e(n+1);
    for(int i = 1;i <= m; i++){
        int a,b,c;cin>>a>>b>>c;
        e[a].push_back({b,c});
    }
    auto dfs = [&](auto dfs,int u)->ld{
        if(u == n) return 0;
        if(dp[u]) return dp[u];
        for(auto [v,w]:e[u]){
            dp[u] += (dfs(dfs,v) + w)*1.0/e[u].size();
        }
        return dp[u];
    };
    dfs(dfs,1);
    cout<<fixed<<setprecision(2)<<dp[1];
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

# 2026.4.10 **小红的图上加边**

题目链接：https://www.nowcoder.com/practice/28c35b0e3f3b4a20aee8f0497ca6745e?channelPut=tracker2

知识点：贪心，并查集

我们先用并查集将已经连接的边合并起来，并且更新这个区间的最大值，然后我们再遍历一遍n个节点，将每个连通块的代表节点(fa[i]==i)加入到remain数组中，接下来我们只需要把这些代表点连接起来即可，由于连接的代价是新形成的联通块的最大元素值 ，我们需要最小代价，我们可以贪心想到对这些点的最大元素值从小到大排序，从头连到尾，这样代价就是除去第一个点代价的总代价。

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ld long double
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;
const int N = 1e5 + 10;
int fa[N],w[N];
int find(int x){
    if(fa[x] == x) return x;
    return fa[x] = find(fa[x]);
}
void merge(int x,int y){
    int fx = find(x),fy = find(y);
    if(fx != fy){
        fa[fx] = fy;
        w[fy] = max(w[fy],w[fx]);
    }
}
void init(){
    for(int i = 1;i < N; i++) fa[i] = i;
}
void solve(){
    int n,m;cin>>n>>m;
    for(int i = 1;i <= n; i++){
        int x;cin>>w[i];
    }
    int cur = -1;
    for(int i = 1;i <= m; i++){
        int u,v;cin>>u>>v;
        merge(u,v);
    }
    int ans = 0;
    vector<int> remain;
    for(int i = 1;i <= n; i++){
        if(fa[i] == i) remain.push_back(w[i]);
    }
    sort(remain.begin(),remain.end());
    for(int i = 1;i < remain.size(); i++) ans += remain[i];
    cout<<ans;
}
signed main(){
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(nullptr);
    init();
    int t = 1;
    // cin>>t;
    while(t--){
        solve();
    }return 0;
}
~~~

