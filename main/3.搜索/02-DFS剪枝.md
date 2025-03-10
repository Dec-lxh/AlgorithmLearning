## 剪枝

其实就是将搜索过程当中一些不必要的部分直接剔除掉，因为搜索过程构成了一棵树，剔除不必要的部分，就像是在树上将树枝剪掉，故名剪枝。
剪枝是回溯法的一种重要优化手段，方法往往先写一个暴力搜索，然后找到某些特殊的数学关系，或者逻辑关系，通过它们的约束让搜索树尽可能浅而小，从而达到降低时间复杂度的目的。
一般来说，剪枝的复杂度难以计算。

## 例1
问题描述
数字王国开学了，它们也和我们人类一样有开学前的军训，现在一共有 n名学生，每个学生有自己的一个名字ai（数字王国里的名字就是一个正整数，注意学生们可能出现重名的情况），此时叛逆教官来看了之后感觉十分别扭，决定将学生重新分队。
排队规则为：将学生分成若干队，每队里面至少一个学生，且每队里面学生的名字不能出现倍数关系（注意名字相同也算是倍数关系）。现在请你帮忙算算最少可以分成几队？

输入格式
第一行包含一个正整数 n，表示学生数量。
第二行包含 n个由空格隔开的整数，第 i 个整数表示第 i 个学生的名字 ai。

输出格式
输出共 1行，包含一个整数，表示最少可以分成几队。
```
#include<bits/stdc++.h>
using namespace std;
#define ll long long
#define endl '\n'
const int N = 15;
int n, a[N];
vector<int> v[N]; //v[i]存队伍i中所有人的编号，
                  //比如v[1]存队伍1中所有人的编号


//cnt表示队伍数量，dfs返回在cnt个队伍的情况下是否可以成功分组
bool dfs(int cnt, int x) {
    if (x == n + 1) { //每个人都成功分组
        // 检查当前方案的合法性
      for(int i = 1; i <= cnt; ++i)
      {
          for(int j = 0; j < v[i].size(); ++j)
          {
              for(int k = j + 1; k < v[i].size(); ++k)
              {
                 if(v[i][k] % v[i][j] == 0) return false;
              }
          }
      }   
    return true;
    }

    //枚举每个人所属的队伍
    for (int i = 1; i <= cnt; i++) {
        v[i].push_back(a[x]);
        if (dfs(cnt, x + 1)) return true;
        v[i].pop_back(); //恢复现场
    }
    return false;
}

int main() {
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    sort(a + 1, a + n + 1);
    for (int i = 1; i <= n; i++) {
        if (dfs(i, 1)) {
            cout << i << endl;
            break;
        }
    }
    return 0;
} 
```
剪枝后
```
#include<bits/stdc++.h>
using namespace std;
#define ll long long
#define endl '\n'
const int N = 15;
int n, a[N];
vector<int> v[N]; //v[i]存队伍i中所有人的编号，
                  //比如v[1]存队伍1中所有人的编号


//cnt表示队伍数量，dfs返回在cnt个队伍的情况下是否可以成功分组
bool dfs(int cnt, int x) {
    if (x == n + 1) { //每个人都成功分组
        return true;
    }

    //枚举每个人所属的队伍
    for (int i = 1; i <= cnt; i++) {
        int f = 0;
        for (auto j : v[i]) {
            if (a[x] % j == 0) {
                f = 1;
                break;
            }
        }
        if (f) continue;
        v[i].push_back(a[x]);
        if (dfs(cnt, x + 1)) return true;
        v[i].pop_back(); //恢复现场
    }
    return false;
}

int main() {
    ios::sync_with_stdio(0), cin.tie(0), cout.tie(0);
    cin >> n;
    for (int i = 1; i <= n; i++) cin >> a[i];
    sort(a + 1, a + n + 1);
    for (int i = 1; i <= n; i++) {
        if (dfs(i, 1)) {
            cout << i << endl;
            break;
        }
    }
    return 0;
}
```