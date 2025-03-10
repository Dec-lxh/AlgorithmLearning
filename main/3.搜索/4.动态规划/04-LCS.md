## 最长公共子序列算法模型

最长公共子序列（LCS）是一个经典的动态规划模型，用于求解两个序列的最长公共子序列。 

LCS算法的时间复杂度为O(N^2)，其中N是序列的长度。 

LCS问题可以扩展到求解具体子序列的问题。

## LCS算法状态定义和转移方程

状态定义：dp[i][j]表示序列a的前i个字符和序列b的前j个字符的最长公共子序列的长度。 

转移方程：当a[i]等于b[j]时，dp[i][j]=dp[i-1][j-1]+1；否则，dp[i][j]=max(dp[i-1][j], dp[i][j-1])。 

初始条件：dp[][j]和dp[i][0]都为0。

## 例题1：最长公共子序列

![输入图片说明](https://cdn.jsdelivr.net/gh/Dec-lxh/Images@main/img/20250310104747.png)

```
#include <bits/stdc++.h>
using namespace std;
const int N = 1e3 + 9;

int n, m, a[N], b[N], dp[N][N];

int main() {
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; ++i) cin >> a[i];
    for (int i = 1; i <= m; ++i) cin >> b[i];

    for (int i = 1; i <= n; ++i) {
        for (int j = 1; j <= m; ++j) {
            if (a[i] == b[j]) dp[i][j] = dp[i - 1][j - 1] + 1;
            else dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
        }
    }

    cout << dp[n][m] << '\n';
    return 0;
}
```

## 求解具体子序列的方法

```
#include <bits/stdc++.h>
using namespace std;
using ll = long long;
const ll p = 1e9 + 7;
const int inf = 1e9, N = 1e3 + 9;

int a[N], b[N], dp[N][N];

int n, m;
cin >> n >> m;
for(int i = 1; i <= n; ++ i)cin >> a[i];
for(int i = 1; i <= m; ++ i)cin >> b[i];
for(int i = 1; i <= n; ++ i)
{
    for(int j = 1; j <= m; ++ j)
    {
        if(a[i] == b[j])dp[i][j] = dp[i - 1][j - 1] + 1;
        else dp[i][j] = max(dp[i][j - 1], dp[i - 1][j]);
    }
}
vector<int> v;
int x = n, y = m;
while(x && y)
{
    if(a[x] == b[y])
    {
        v.push_back(a[x]);
        x --, y --;
    }else if(dp[x - 1][y] > dp[x][y - 1])x --;
    else y --;
}
reverse(v.begin(), v.end());
for(const auto &i : v)cout << i << ' ';
return 0;
```

