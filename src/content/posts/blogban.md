# 1	基础算法

## 1.1	头文件

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ld long double
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;

void solve(){
    
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

## 1.2	常用函数

### 1.2.1	组合数预处理

~~~cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
// 常量定义
const int INF = 0x3f3f3f3f3f3f3f3f;
const int mod = 1e9 + 7;
const int mx = 1e6 + 1000;
int fac[mx + 1], ifac[mx + 1];
//快速幂运算 x^p % mod
int fastpow(int x, int p) {
    int ans = 1;
    x %= mod;
    while (p) {
        if (p & 1) ans = ans * x % mod;
        x = x * x % mod;
        p >>= 1;
    }
    return ans;
}
//费马小定理求单个数的逆元
int inv(int x) {
    return fastpow(x, mod - 2);
}
//预处理阶乘和阶乘逆元，复杂度: O(MX + log mod)
void init() {
    fac[0] = 1;
    for (int i = 1; i <= mx; i++) {
        fac[i] = fac[i - 1] * i % mod;
    }   
    // 关键：先求出最大阶乘的逆元，再逆推回去
    ifac[mx] = inv(fac[mx]);
    for (int i = mx - 1; i >= 0; i--) {
        ifac[i] = ifac[i + 1] * (i + 1) % mod;
    }
}

//C(a, b) = a! / (b! * (a-b)!) % mod
int c(int a, int b) {
    if (b < 0 || b > a) return 0;
    return fac[a] * ifac[b] % mod * ifac[a - b] % mod;
}
void solve() {
    // 示例：计算 C(10, 3)
    // cout << c(10, 3) << endl;
}
signed main() {
    // 关流加速
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(nullptr);
    // 必须先调用预处理
    init();
    int t = 1;
    cin >> t;
    while(t--) solve();
    return 0;
}
~~~

### 1.2.2	整数二分

~~~cpp
int find(x){
    int l = 0, r = n + 1;
    while(l + 1 < r){
        int mid = l+r>>1;
        if(a[mid] <= q) l = mid;
        else r = mid;
    }
    return l;
}
~~~

### 1.2.3	浮点数二分

~~~cpp
ld find(ld x){
    ld l = -100, r = 100;
    while(r - l > 1e-5){
        ld mid = (l + r)/2;
        if(check(mid)) l = mid;
        else r = mid;
    }
    return l;
}
~~~

###  1.2.3 	判断素数

~~~cpp
bool isprime(int x) {
    if (x == 1) return false;
    for (int i = 2; i * i <= x; ++i)
        if (x % i == 0)
            return false;
    return true;
}
~~~



# 2	数论

## 2.1	线性筛素数

### 2.1.1	埃式筛

 埃氏筛的时间复杂度为 O(nloglogn)，在处理 1e7 以内的数据量时表现非常出色。 

~~~cpp
const int mx = 2e5+10;
bool heshu[mx];
int zhishu[mx];
int cnt;//计数器
void sieve(int n){
    for(int i = 2; i <= n; i++){
        if(!heshu[i]){
            cnt++;
            zhishu[cnt] = i;//注意是从1开始的
            for(int j = i * i; j <= n; j += i){
                heshu[j] = 1;
            }
        }
    }
}
~~~

## 2.2	费马小定理

 若 p为质数，且a,p 互质，则 𝑎𝑝−1 ≡1(𝑚𝑜𝑑 𝑝)

 𝑎 ∗𝑎𝑝−2 = 𝑎𝑝−1 ≡ 1(𝑚𝑜𝑑 𝑝)

 所以快速幂求 a 模意义下的逆元就是 fastpow(a,mod-2) 只适用于 p 为质数

## 2.3	 裴蜀定理 

 对于一个二元一次方程*ax*+*by*=*c*，如果 **c是gcd(a,b)的倍数**，那么**这个方程一定有整数解** 

 对于一个 **n元一次不定方程** *a*1*x*1+*a*2*x*2+*a*3*x*3+⋯+*a**n**xn*=*c*，*c*是gcd(*a*1,*a*2,*a*3,⋯,*an*)的倍数，是这个方程有整数解的充要条件 

## 2.4	快速幂

~~~cpp
int fastpow(int a,int p,int mod){
    int ans = 1;
    a %= mod;
    while(p){
        if(b % 2 == 1){
            ans = ans * a % c;
        }
        a = a * a % c;
        b >>= 1;
    }
    return ans;
}
~~~

## 2.5	求逆元

p需要是质数

~~~cpp
int getinv(int x,int p){
    return fastpow(x,p - 2)
}
~~~

## 2.6	扩展欧几里得

待补充

~~~cpp
int exgcd(int a,int b,int &x,int &y){
    if(b==0){
        x=1,y=0;
        return a;
    }
    int x1,y1,d;
    d=exgcd(b,a%b,x1,y1);
    x=y1,y=x1-a/b*y1;
    return d;
}
~~~



## 2.7	矩阵快速幂



~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;
const int mod=1e9+7;
int n,k;
//矩阵快速幂
struct matrix{
    int c[101][101];//设置矩阵大小
    matrix(){memset(c,0,sizeof(c));}
}res,a;
matrix operator*(matrix &x,matrix &y){
    matrix t;
    for(int i=1;i<=n;i++){//n大小记得换
        for(int k=1;k<=n;k++){//把k和j交换可以优化常数
            for(int j=1;j<=n;j++){
                t.c[i][j]=(t.c[i][j]+x.c[i][k]*y.c[k][j])%mod;//注意模数
            }
        }
    }
    return t;//注意返回
};
void fastpow(int k){
    for(int i=1;i<=n;i++) res.c[i][i]=1;
    while(k){
        if(k&1) res=res*a;
        a=a*a;
        k>>=1;
    }
}
void solve(){
    cin>>n>>k;
    for(int i=1;i<=n;i++){
        for(int j=1;j<=n;j++){
            cin>>a.c[i][j];
        }
    }
    fastpow(k);
    for(int i=1;i<=n;i++){
        for(int j=1;j<=n;j++){
            cout<<res.c[i][j]<<" ";
        }
        cout<<"\n";
    }
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



# 3	图论

## 3.1	 单源最短路径 

### 3.1.1	 Djikstra算法 

~~~cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
int n,m,s;
const int INF=1e18;
vector<pair<int,int>> e[101010];
auto dij(){
    vector<int> dist(n+1,INF);
    dist[s]=0;
    priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> q;
    q.push({0,s});
    while(q.size()){
        auto [d,u]=q.top();q.pop();
        if(d>dist[u]) continue;
        for(auto [v,w]:e[u]){
            if(dist[v]>d+w){
                dist[v]=d+w;
                q.push({dist[v],v});
            }
        }
    }
    return dist;
}
void solve(){
    cin>>n>>m>>s;
    while(m--){
        int u,v,w;
        cin>>u>>v>>w;
        e[u].push_back({v,w});
    }
    auto dist=dij();
    for(int i=1;i<=n;i++) cout<<dist[i]<<" ";

}
signed main(){
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(nullptr);
    int t=1;
    // cin>>t;
    while(t--){
        solve();
    }return 0;
}
~~~

## 3.2	 最小生成树 

在一个带权无向图中
找一棵权值和最小的生成树 

1 所有点都连通
2 没有环
3 有 n-1 条边 

### 3.2.1	 Prim算法 O(m log n)

 Prim的核心思想:  每次选择连接已选点集合 和 未选点集合之间的最小边 

~~~cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long

const int N = 200010;

vector<pair<int,int>> g[N]; // {邻点, 权值}
bool vis[N];

signed main(){
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, m;
    cin >> n >> m;

    for(int i = 1; i <= n; i++) g[i].clear();

    for(int i = 0; i < m; i++){
        int u, v, w;
        cin >> u >> v >> w;
        g[u].push_back({v, w});
        g[v].push_back({u, w}); // 无向图
    }

    priority_queue<
        pair<int,int>,
        vector<pair<int,int>>,
        greater<pair<int,int>>
    > q;

    int ans = 0, cnt = 0;

    q.push({0, 1}); // 从1开始

    while(!q.empty()){
        auto [w, u] = q.top();
        q.pop();

        if(vis[u]) continue;

        vis[u] = 1;
        ans += w;
        cnt++;

        for(auto [v, ww] : g[u]){
            if(!vis[v]){
                q.push({ww, v});
            }
        }
    }

    if(cnt != n) cout << "orz\n"; // 不连通
    else cout << ans << "\n";
}
~~~

## 3.2.2	 Kruskal 算法  O(m log m) 

 Kruskal 算法核心思想 ： 每次选当前最小的边，只要不形成环就加入 ，直到 选了 n-1 条边 

 因为 **树一定有 n-1 条边**。  这个算法是 **贪心算法**：每一步都选当前最小的边。 

~~~cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N = 200010;
int fa[N];
int find(int x){
    if(fa[x] == x) return x;
    return fa[x] = find(fa[x]); // 路径压缩
}
struct Edge{
    int u, v, w;
};
signed main(){
    ios::sync_with_stdio(false);
    cin.tie(nullptr);
    int n, m;
    cin >> n >> m;
    // 初始化并查集
    for(int i = 1; i <= n; i++) fa[i] = i;
    vector<Edge> e(m);
    for(int i = 0; i < m; i++){
        cin >> e[i].u >> e[i].v >> e[i].w;
    }
    // 按权值排序
    sort(e.begin(), e.end(), [](Edge a, Edge b){
        return a.w < b.w;
    });
    int ans = 0;
    int cnt = 0;
    for(auto [u, v, w] : e){
        int fu = find(u);
        int fv = find(v);
        if(fu == fv) continue; // 成环跳过
        fa[fu] = fv;           // 合并
        ans += w;
        cnt++;
        if(cnt == n - 1) break; // 已构成 MST
    }
    if(cnt != n - 1) cout << "orz\n"; // 不连通
    else cout << ans << "\n";
}
~~~

## 3.3	拓扑排序

拓扑排序是一个有向无环图的所有顶点的线性序列。

该序列需要满足每个顶点出现且**只出现一次**和如果有一条 *A* 到 *B* 的路径，在序列中 *A* 出现在 *B* 的前面。

拓扑排序的步骤：

- 计算每个点的入度。
- 入度为 0 就加入队列。
- 当队列不为空则循环：
  - 取出队首元素并输出。
  - 遍历队首元素的连边，对应节点的入度 −1。
  - 当对应的节点入度为 0 就加入队列。

~~~cpp
void solve(){
    int n; cin >> n;
    vector<int> deg(n + 1);          // 入度数组
    vector<vector<int>> e(n + 1);   // 邻接表
    
    for(int i = 1; i <= n; i++){
        int x;
        while(cin >> x){
            if(x == 0) break;
            e[i].push_back(x);      // 建图
            deg[x]++;               // 统计入度
        }
    }
    
    queue<int> q;
    for(int i = 1; i <= n; i++){
        if(!deg[i]) q.push(i);      // 入度为 0 的点入队
    }
    
    while(q.size()){
        int t = q.front(); q.pop();
        cout << t << " ";           // 输出/记录拓扑序
        
        for(auto i : e[t]){
            deg[i]--;               // 删边：终点入度减 1
            if(!deg[i]) q.push(i);  // 新入度为 0 的点入队
        }
    }
}
~~~

# 4	数据结构

## 4.1	并查集

 merge时将size小的往size大的上面合并有利于降低树高 

使用sz时需要判断是不是代表点(fa[x]==x)

~~~cpp
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
        }
        else{
            fa[fx] = fy;
            sz[fy] += sz[fx];
        }
    }
}
~~~

## 4.2	中序遍历+前后序遍历建树

~~~cpp
//分层次遍历
void solve(){
    int n;
    cin >> n;
    map<int,int> insuf,inmid;
    vector<int> suf(n + 1),mid(n + 1);
    for(int i = 1;i <= n; ++i){
        cin >> suf[i];
        insuf[suf[i]] = i;
    }
    for(int i = 1;i <= n; ++i){
        cin >> mid[i];
        inmid[mid[i]] = i;
    }
    map<int,int> l,r;
    auto find = [&](int pl, int pr){
        int best = -INF;
        for(int i = pl;i <= pr; ++i){
            int val = mid[i];
            if(insuf[val] > best) best = insuf[val];
        }
        return suf[best];
    };
    auto built = [&](auto built, int pl, int pr)->int{
        if(pl > pr) return -1;
        int root = find(pl, pr);
        int pos = inmid[root];
        l[root] = built(built, pl, pos - 1);
        r[root] = built(built, pos + 1, pr);
        return root;
    };
    built(built, 1, n);
    int root = find(1, n);
    queue<int> q;
    q.push(root);
    vector<int> ans;
    while(q.size()){
        int cur = q.front();
        q.pop();
        ans.push_back(cur);
        if(l[cur] != -1) q.push(l[cur]);
        if(r[cur] != -1) q.push(r[cur]);
    }
    for(int i = 0;i < ans.size() - 1; ++i) cout << ans[i] << " ";
    cout << ans.back();
}
~~~

# 5	动态规划

## 5.1 最长不下降子序列 (LNDS)  

~~~cpp
int main() {
    int n;
    cin >> n;
    vector<int> a(n+1);
    for (int i = 1; i <= n; i++) cin >> a[i];
    vector<int> d;  // d[k]：长度 k+1 的 LNDS 的最小结尾
    // LNDS (不下降): 使用 upper_bound 找到第一个 > x 的位置替换
    // LIS (严格上升): 则改为 lower_bound 找到第一个 >= x 的位置替换
    for (int i = 1; i <= n; i++) {
        int x = a[i];
        auto it = upper_bound(d.begin()+1, d.end(), x);
        if (it == d.end()) {
            d.push_back(x);
        } else {
            *it = x;
        }
    }
    cout << d.size() << endl;
    return 0;
}
~~~

## 5.2	期望dp

~~~cpp
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
~~~

## 5.3	LCS (最长公共子序列)  

~~~cpp
void solve() {
    string s, t;
    cin >> s >> t;

    int n = s.size();
    int m = t.size();

    // dp[i][j] 表示 s 的前 i 个字符与 t 的前 j 个字符的最长公共子序列长度
    // 这里的下标直接用 0 到 n，dp 大小开 (n+1) * (m+1)
    vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));

    // 1. 动态规划填表
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            if (s[i - 1] == t[j - 1]) { // 注意字符串下标从 0 开始，所以是 i-1 和 j-1
                dp[i][j] = dp[i - 1][j - 1] + 1;
            } else {
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }

    // 2. 倒序回溯构造具体序列
    string ans = "";
    int i = n, j = m;
    while (i > 0 && j > 0) {
        if (s[i - 1] == t[j - 1]) {
            ans += s[i - 1]; // 发现公共字符
            i--;
            j--;
        } else {
            // 往 dp 值更大的方向回退
            if (dp[i - 1][j] >= dp[i][j - 1]) {
                i--;
            } else {
                j--;
            }
        }
    }

    // 因为是倒序回溯，最后需要反转字符串
    reverse(ans.begin(), ans.end());
    cout << ans << endl;
}
~~~

## 5.4	01背包

~~~cpp
void solve() {
    int n, v;
    cin >> n >> v;
    // dp: 只要容量不超过 j 的最大价值 (初始化为0)
    // dpp: 恰好容量为 j 的最大价值 (初始化为负无穷)
    vector<int> dp(v + 1, 0);
    vector<int> dpp(v + 1, -INF);

    dpp[0] = 0; // 恰好装满容量为 0 的价值是 0

    for (int i = 1; i <= n; i++) {
        int weight, value;
        cin >> weight >> value;
        
        // 0/1 背包逆序遍历，防止重复挑选同一个物品
        for (int j = v; j >= weight; j--) {
            // 变体1：不要求装满
            dp[j] = max(dp[j], dp[j - weight] + value);
            
            // 变体2：恰好装满 (只有当前驱状态可达时才转移)
            if (dpp[j - weight] != -INF) {
                dpp[j] = max(dpp[j], dpp[j - weight] + value);
            }
        }
    }

    // 输出 1：最大价值
    cout << dp[v] << "\n";

    // 输出 2：恰好装满的最大价值
    if (dpp[v] < 0) cout << 0 << "\n"; // 无法恰好装满
    else cout << dpp[v] << "\n";
}
~~~



# 6	杂项

## 6.1	单调栈

~~~cpp
void solve() {
    int n;
    cin >> n;
    vector<int> a(n + 1);
    vector<int> st;      // 单调栈：存储下标
    vector<int> f(n + 1); // 存储结果：右侧第一个比 a[i] 大的元素的下标
    for (int i = 1; i <= n; i++) cin >> a[i];
    // 从右往左遍历
    for (int i = n; i >= 1; i--) {
        // 维护单调性：如果栈顶元素不比当前元素大，它就不可能是左边元素的“第一个更大值”，弹出
        while (!st.empty() && a[st.back()] <= a[i]) {
            st.pop_back();
        }
        // 栈顶就是右侧第一个比 a[i] 大的下标
        if (!st.empty()) {
            f[i] = st.back();
        } else {
            f[i] = 0; // 说明右侧没有比它更大的
        }
        // 将当前下标入栈，供左侧元素参考
        st.push_back(i);
    }
}
~~~

