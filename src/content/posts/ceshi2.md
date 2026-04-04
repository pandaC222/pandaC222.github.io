# 【必填】文章标题
title: 我的第二篇博客

# 【必填】发布日期，格式必须为 YYYY-MM-DD
published: 2026-04-04

# 【可选】文章描述，会显示在首页卡片上
description: 仍然用来测试功能

# 【可选】文章封面图路径
# 1. 外部图片：http://...
# 2. 本地图片：/assets/images/xxx.png (放在 public 文件夹下)
image: '/assets/home/nhome.webp'

# 【可选】文章标签，用英文逗号分隔
tags: [算法, C++, 随笔]

# 【可选】文章分类
category: 算法

# 【可选】是否置顶，true 为置顶
pinned: false

# 【可选】置顶优先级，数字越小越靠前 (0, 1, 2...)
priority: 0

# 【必填】草稿状态。true 为隐藏，发布时必须改为 false

draft: false

## 	测试内容：

主要测试标签和目录功能
以及代码块功能

```cpp
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ld long double
#define debug(x) cerr << #x << ": " << x << '\n';
const int INF = 0x3f3f3f3f3f3f3f3f;

void solve(){
    cout<<"这是我的blog";
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
```

