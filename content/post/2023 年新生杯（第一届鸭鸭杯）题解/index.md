+++
slug = "2023-new-year-cup-1st-round"
title = '2023 年新生杯（第一届鸭鸭杯）题解'
date = 2024-09-09T23:49:57+08:00
weight=6

categories = [
    "题解"
]

+++

- [Ivan\_Chien](#ivan_chien)
  - [C++](#c)
    - [A](#a)
    - [B](#b)
    - [C](#c-1)
    - [D](#d)
    - [E](#e)
    - [F](#f)
    - [G](#g)
    - [H](#h)
    - [i](#i)
    - [J](#j)
  - [Python 参考](#python-参考)
    - [C](#c-2)
  - [Java 参考](#java-参考)
    - [A](#a-1)

## Ivan_Chien

### C++

#### A

签到题。

```c
#include <iostream>
#include <climits>
 
int main()
{
    int n, t;
    std::cin >> n >> t;
 
    int prev = INT_MIN / 2;
    int curr;
    while (std::cin >> curr)
    {
        if (curr - prev <= t)
        {
            std::cout << curr << std::endl;
            return 0;
        }
        prev = curr;
    }
 
    std::cout << -1 << std::endl;
     
    return 0;
}
```

#### B

模拟。有多对可消时，易证消的顺序不影响最后结果。

```c
#include <bits/stdc++.h>
using i64 = long long;
 
int main()
{
    int n;
    std::cin >> n;
    std::vector<int> v(n);
 
    for (int i = 0; i < n; ++i)
    {
        std::cin >> v[i];
    }
 
    i64 ans = 0;
    bool flag = true;
    while (flag)
    {
        flag = false;
        for (int i = 0; i + 1 < n; ++i)
        {
            if (v[i] == v[i + 1])
            {
                flag = true;
                ans += 1LL * v[i];
                v.erase(v.begin() + i);
                v.erase(v.begin() + i);
                n -= 2;
                break;
            }
        }
    }
 
    std::cout << ans << std::endl;
     
    return 0;
}
```

#### C

两两相消，使用 map 来维护数的库存。排序后用双指针亦可。

```c
#include <bits/stdc++.h>
using i64 = long long;
 
int main()
{
    int n, sum;
    std::cin >> n >> sum;
 
    std::map<int, int> cnt;
    i64 ans = 0;
    for (int i = 0; i < n; ++i)
    {
        int a;
        std::cin >> a;
        if (cnt[sum - a] > 0)
        {
            --cnt[sum - a];
            ++ans;
        }
        else
        {
            ++cnt[a];
        }
    }
 
    std::cout << ans << std::endl;
     
    return 0;
}
```

#### D

统计字母数量是否足够即可。

```c
#include <bits/stdc++.h>
using i64 = long long;
 
int main()
{
    int n, m;
    std::string a, b;
    std::cin >> n >> m >> a >> b;
 
    std::map<char, int> cnt;
    for (auto c : a)
    {
        ++cnt[c];
    }
 
    for (auto c : b)
    {
        if (cnt[c] <= 0)
        {
            std::cout << "NO" << std::endl;
            return 0;
        }
        --cnt[c];
    }
 
    std::cout << "YES" << std::endl;
     
    return 0;
}
```

#### E

贪心。从 0 出发，对石头高度排序，每次往序列的另一头跳即可。

```c
#include <bits/stdc++.h>
using i64 = long long;
 
int main()
{
    int n, m;
    std::cin >> n >> m;
    std::vector<int> v(n);
 
    for (int i = 0; i < n; ++i)
    {
        std::cin >> v[i];
    }
     
    std::sort(v.begin(), v.end());
 
    int left = 0, right = n;
    int currH = 0;
    i64 ans = 0;
    while (left < right)
    {
        int d1 = std::abs(currH - v[left]);
        int d2 = std::abs(currH - v[right - 1]);
        if (d1 > d2)
        {
            ans += 1LL * d1;
            currH = v[left];
            ++left;
        }
        else   // d1 < d2, NEVER EQUAL
        {
            ans += 1LL * d2;
            currH = v[right - 1];
            --right;
        }
    }
 
    if (ans <= m)
    {
        std::cout << "算你厉害" << std::endl;
    }
    else
    {
        std::cout << ans - m << std::endl;
    }
     
    return 0;
}
```

#### F

枚举所有区间和即可，用前缀和做个简单优化。

```c
#include <bits/stdc++.h>
using i64 = long long;
 
int main()
{
    int n, m;
    std::cin >> n >> m;
 
    std::vector<int> pref(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        int a;
        std::cin >> a;
        pref[i] = a + pref[i - 1];
    }
 
    i64 ans = 0;
    for (int i = 1; i <= n; ++i)
    {
        for (int j = 0; j < i; ++j)
        {
            if (pref[i] - pref[j] == m)
            {
                ++ans;
            }
        }
    }
 
    std::cout << ans << std::endl;
     
    return 0;
}
```

#### G

模拟。

```c
#include <bits/stdc++.h>
using i64 = long long;

int main()
{
    int n, m;
    std::cin >> n >> m;
 
    std::vector mat(n, std::vector(m, 0));
 
    for (auto& v : mat)
    {
        for (auto& a : v)
        {
            std::cin >> a;
        }
    }
 
    int cq;
    std::cin >> cq;
    std::vector<int> q(m);
    while (cq--)
    {
        int ans = 0;
        for (int i = 0; i < m; ++i)
        {
            std::cin >> q[i];
        }
     
        for (int i = 0; i < n; ++i)
        {
            bool flag = true;
            for (int j = 0; j < m; ++j)
            {
                if (q[j] != -1 && q[j] != mat[i][j])
                {
                    flag = false;
                    break;
                }
            }
            if (flag) ++ans;
        }
        std::cout << ans << std::endl;
    }
     
    return 0;
}
```

#### H

简单构造。

```c
#include <bits/stdc++.h>
using i64 = long long;
 
int main()
{
    i64 n, m;
    std::cin >> n >> m;
    i64 ans = 0;
 
    while (n != m)
    {
        if (n < m)
        {
            std::swap(n, m);
        }
        i64 f = n / m;
        if (f * m == n) --f;
        n -= f * m;
        ans += f;
    }
 
    std::cout << ans << std::endl;
     
    return 0;
}
```

#### i

前缀和。

```c
#include <bits/stdc++.h>
using i64 = long long;
 
int main()
{
    i64 n, w;
    std::cin >> n >> w;
 
    std::vector<int> pref(n + 1);
    for (int i = 1; i <= n; ++i)
    {
        int a;
        std::cin >> a;
        pref[i] = a + pref[i - 1];
    }
 
    int max = -1;
    for (int i = w; i <= n; ++i)
    {
        max = std::max(max, pref[i] - pref[i - w]);
    }
    std::cout << max << std::endl;
     
    return 0;
}
```

#### J

数据范围小，直接暴力。正统做法大概是 unique 后做区间 DP。

```c
#include <bits/stdc++.h>
using i64 = long long;
 
int main()
{
    std::string s;
    std::cin >> s;
 
    int ans_odd = 0, ans_even = 0;
    int n = s.length();
    for (int d = 1; d <= n; ++d)
    {
        for (int i = 0; i + d <= n; ++i)
        {
            auto ss = s.substr(i, d);
            ss.erase(std::unique(ss.begin(), ss.end()), ss.end());
            int nn = ss.length();
            bool flag = true;
            for (int i = 0; i < nn / 2; ++i)
            {
                if (ss[i] != ss[nn - 1 - i])
                {
                    flag = false;
                    break;
                }
            }
            if (flag)
            {
                if (d & 1) ++ans_odd;
                else ++ans_even;
            }
        }
    }
 
    std::cout << ans_even << ' ' << ans_odd << std::endl;
     
    return 0;
}
```

### Python 参考

#### C

```python
from collections import Counter
 
n, m = map(int, input().split())
c = Counter()
ans = 0
for _ in range(n):
    a = int(input())
    if c[m - a] > 0:
        c[m - a] -= 1
        ans += 1
    else:
        c[a] += 1
print(ans)
```

### Java 参考

#### A

```java
import java.util.Scanner;
 
public class Main {
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        int n = s.nextInt();
        int m = s.nextInt();
        int prev = -114514191;
        for (int i = 0; i < n; i++)  {
            int a;
            a = s.nextInt();
            if (a - prev <= m) {
                System.out.println(a);
                return ;
            }
            prev = a;
        }
        System.out.println(-1);
    }
}
```


