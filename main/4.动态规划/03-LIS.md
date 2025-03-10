## 最长上升子序列算法模型

LIS（最长上升子序列）是一个经典的DP（动态规划）模型。 

子序列指的是在一个序列中，按照原顺序选出若干个不一定连续的元素所组成的序列。 

LIS的时间复杂度为O(N^2)，还有一种利用二分实现的O(NlogN)时间复杂度的模型。

一般设dp[i]表示1~i序列中以a[i]结尾的最长上升子序列的长度。 

状态转移方程为dp[i] = max(dp[j] + 1)，其中j < i且a[j] < a[i]。 

表示a[i]可以插入到不同的子序列后面，决定是否可以连在一起。

## 例题1：蓝桥勇士

![输入图片说明](https://cdn.jsdelivr.net/gh/Dec-lxh/Images@main/img/20250310104731.png)

```
#include <bits/stdc++.h>
using namespace std;
const int N = 1e3+5;

int a[N], dp[N];

int main()
{
  int n; cin >> n;
  for(int i = 1; i <= n; ++i)
  {
    cin >> a[i];
  }
  for(int i = 1; i <= n; ++i){
    dp[i]=1;
    for(int j = 1; j <= i; ++j){
      if(a[i]>a[j])dp[i]=max(dp[i],dp[j]+1);
    }
  }
  int ans=0;
  for(int i = 1; i <= n; ++i){
    ans = max(ans ,dp[i]);
  }
  cout<<ans<<endl;
  return 0;
}
```

## 例题2：合唱队形

![输入图片说明](https://cdn.jsdelivr.net/gh/Dec-lxh/Images@main/img/20250310104739.png)

```
#include<bits/stdc++.h>
using namespace std;
const int N=103;

int a[N],dpl[N], dpr[N];

int main()
{
  int n; cin >> n;
  for(int i = 1; i <= n; ++i)cin >> a[i];
  for(int i = 1; i <= n; ++i)
  {
    dpl[i]=1;
    for(int j = 1; j < i; ++j) if(a[i] > a[j])dpl[i] = max(dpl[i], dpl[j]+1 );
  }
  for(int i = n; i >= 1; --i)
  {
    dpr[i]=1;
    for(int j = i+1; j <= n; ++j) if(a[i] > a[j])dpr[i] = max(dpr[i], dpr[j]+1 );
  }
  int ans=n;
  for(int i = 1; i <= n; ++i) ans = min(ans , n-(dpl[i]+dpr[i]-1));
  cout<<ans<<endl;
  return 0;
}
```

