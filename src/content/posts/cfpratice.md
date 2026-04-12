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

# 2026.4.8 Gellyfish and Baby's Breath 

题目链接：https://codeforces.com/contest/2116/problem/B

难度：1300

知识点：快速幂，堆

给我们两个排列，需要求出按照公式求出r中每个元素能取得的最大值，我们可以想到，2的幂次越大，值越大，指数是爆发式增长，每多增加一次就会爆发增长一次，所以记录前缀最大次数很关键，但是我们可能会遇到q中最大次数和p中最大次数相同，这时我们就要比较其对应的另一个p[i]或者q[i]的大小，选大的，我们用最大堆qtop，ptop来维护记录q和p前缀最大值的过程，每次i增加一项就把值和下标push进堆，然后求的时候取出堆顶比较次数即可，比较完后去求r[i]。

代码如下（cpp）：

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ld long double
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;
const int mod = 998244353;
int fastpow(int x, int p){
    int ans = 1;
    x %= mod;
    while(p){
        if(p&1) ans = ans * x % mod;
        p >>= 1;
        x = x * x %mod;
    }
    return ans % mod;
}
void solve(){
    int n;cin>>n;
    vector<int> p(n),q(n),r(n);
    priority_queue<pair<int,int>> ptop,qtop;
    for(int i = 0;i < n; i++) cin>>p[i];
    for(int i = 0;i < n; i++) cin>>q[i];
    for(int i = 0;i < n; i++){
        ptop.push({p[i],i});
        qtop.push({q[i],i});
        auto qt = qtop.top();
        auto pt = ptop.top();
        int xq = qt.first,yq = p[i-qt.second];
        int xp = pt.first,yp = q[i-pt.second];
        bool okp = 1;
        if(xq > xp or xq == xp and yq > yp) okp = 0;
        if(okp) r[i] = (fastpow(2,pt.first) + fastpow(2,q[i-pt.second])) % mod;
        else r[i] = (fastpow(2,qt.first) + fastpow(2,p[i-qt.second])) % mod;
    }
    for (auto i : r) cout<<i<<" ";
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

# 2026.4.12 Stamina 

上次写竟然已经是4.8号了吗，我好fvv

题目链接：https://codeforces.com/gym/106394/problem/D

难度：1300

知识点：贪心，堆

这个贪心是预知未来的贪心，就是你先往前走，体力不够了<0了就回头看，找到a[i]最大的地方休息，意思就是你在a[i]最大的地方多休息了一次，实际上还是走到了这里，休息天数加上走了n-1步就是答案了

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ld long double
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;

void solve(){
    int n;
    cin >> n;
    vector<int> a(n + 1);
    for(int i = 1;i <= n; ++i) cin >> a[i];
    priority_queue<int> q;
    int cur = 0, rd = 0;
    for(int i = 1;i <= n - 1; ++i){
        q.push(a[i]);
        auto t = q.top();
        cur--;
        while(cur < 0){
            cur += t;
            rd++;
        }
    }
    cout << rd + n - 1 << "\n";
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

