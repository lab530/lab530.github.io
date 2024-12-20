+++
slug = "2023 Anhui University of Chinese Medicine ACM intramural selection competition solution"
title = '2023 年度安徽中医药大学 ACM 校内选拔赛题解'
date = 2024-09-09T23:49:57+08:00
weight=6

categories = [
    "题解"
]


+++

- [Ivan\_Chien](#ivan_chien)
  - [C++](#c)
    - [A - Roxy Tree](#a---roxy-tree)
    - [B - Variable-like String Literal Check](#b---variable-like-string-literal-check)
    - [C - Push-pop-push-pop](#c---push-pop-push-pop)
    - [D - Balanced Roxy Substring](#d---balanced-roxy-substring)
    - [E - Xepa Predator](#e---xepa-predator)
    - [F - 水王级魔法师](#f---水王级魔法师)
    - [G - 鸭鸭杯](#g---鸭鸭杯)
    - [H - 龙族的传送魔法](#h---龙族的传送魔法)
    - [i - 黄金律法之谜](#i---黄金律法之谜)
    - [J - 开放世界](#j---开放世界)
    - [K - 画家算法](#k---画家算法)
    - [L - 本次比赛的白给题](#l---本次比赛的白给题)
  - [Python](#python)
    - [A](#a)
    - [B](#b)
    - [C](#c-1)
    - [D](#d)
    - [E](#e)
    - [F](#f)
    - [G](#g)
    - [H](#h)
    - [L](#l)
- [Ereflect](#ereflect)
  - [Python](#python-1)
    - [B](#b-1)
    - [C](#c-2)
    - [F](#f-1)

## Ivan_Chien

### C++

#### A - Roxy Tree

跟完全二叉树一样的求。

```cpp
#include <iostream>
#include <map>
#include <limits>
#include <algorithm>
using i64 = long long;

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    std::map<i64, i64> width;
    i64 s = 0LL;
    for (i64 p = 1, v = 1; s < std::numeric_limits<i64>::max() / 10; ++p) {
        s += width[p] = v;
        if (p & 1) v *= 2;
        else v *= 3;
    }

    i64 t;
    while (std::cin >> t) {
        i64 sum = 0LL;
        auto fnd = std::find_if(width.begin(), width.end(), [t, &sum] (auto x) mutable { return t < (sum += x.second); });
        auto [p, v] = *fnd;

        std::cout << p << ' ' << t - (sum - v) + 1 << std::endl;
    }

    return 0;
}
```

#### B - Variable-like String Literal Check

英文签到。

```cpp
#include <iostream>
#include <string>
#include <algorithm>
#include <cctype>
using i64 = long long;

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    int tt;
    std::cin >> tt;
    while (tt--) {
        std::string s;
        std::cin >> s;
        if (!isalpha(s[0]) && s[0] != '_') {
            std::cout << "No" << std::endl;
            continue;
        }
        if (!std::all_of(s.begin() + 1, s.end(), [](char x) { return isalnum(x) || x == '_'; })) {
            std::cout << "No" << std::endl;
            continue;
        }
        std::cout << "Yes" << std::endl;
    }

    return 0;
}
```

#### C - Push-pop-push-pop

模拟。

```cpp
#include <iostream>
#include <deque>
using i64 = long long;

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    int q;
    std::cin >> q;
    std::deque<int> dq;
    while (q--) {
        char instruction;
        std::cin >> instruction;
        int operand;
        switch (instruction) {
        case 's':
        case 'q':
            std::cin >> operand;
            dq.push_back(operand);
            break;
        case 'S':
            if (!dq.empty()) {
                dq.pop_back();
            }
            break;
        case 'Q':
            if (!dq.empty()) {
                dq.pop_front();
            }
            break;
        case 'd':
            if (dq.empty()) {
                std::cout << "empty" << std::endl;
            } else {
                int n = dq.size();
                for (int i = 0; i < n; ++i) {
                    std::cout << dq[i] << ",\n"[i == n - 1];
                }
            }
            break;
        default:
            break;
        }
    }

    return 0;
}
```

#### D - Balanced Roxy Substring

不能算区间 DP 的区间 DP，可以说是记忆化。亦可用滑动窗口。

```cpp
#include <iostream>
#include <string>
#include <array>
#include <vector>
using i64 = long long;

void update(std::array<int, 2>&, const char);
bool check(const std::array<int, 2>&);

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    std::string s;
    std::cin >> s;
    int n = s.length();

    int ans = 0;
    std::vector<std::array<int, 2>> prev(n), f(n);
    for (int i = 0; i + 1 < n; ++i) {
        update(prev[i], s[i]);
        update(prev[i], s[i + 1]);
        if (check(prev[i])) {
            ans = 2;
        }
    }

    for (int d = 2; d < n; ++d) {
        for (int i = 0; i + d < n; ++i) {
            f[i] = prev[i];
            update(f[i], s[i + d]);
            if (d & 1) {
                if (check(f[i])) {
                    ans = 1 + d;
                }
            }
        }
        f.swap(prev);
    }

    std::cout << ans << std::endl;

    return 0;
}

void update(std::array<int, 2>& a, const char c) {
    switch (c) {
    case 'r': ++a[0]; break;
    case 'o': --a[0]; break;
    case 'x': ++a[1]; break;
    case 'y': --a[1]; break;
    }
}

bool check(const std::array<int, 2>& a) {
    return !a[0] && !a[1];
}
```

#### E - Xepa Predator

结构体排序。

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using i64 = long long;

struct Student {
    int id;
    int p, s;
    Student() = default;
    Student(int id, int p, int s) : id{id}, p{p}, s{s} {}
};

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    constexpr int N = 60;
    std::vector<Student> v(N);
    int my_id;
    std::cin >> my_id;
    for (int i = 0; i < N; ++i) std::cin >> v[i].id;
    for (int i = 0; i < N; ++i) std::cin >> v[i].p;
    for (int i = 0; i < N; ++i) std::cin >> v[i].s;

    std::sort(v.begin(), v.end(), [](const Student& a, const Student& b) {
        auto af = 2 * a.p + 1 * a.s;
        auto bf = 2 * b.p + 1 * b.s;
        if (af != bf)
            return af > bf;
        else if (a.p != b.p)
            return a.p > b.p;
        else if (a.s != b.s)
            return a.s > b.s;
        return a.id < b.id;
    });
    
    auto fnd = std::find_if(v.begin(), v.end(), [my_id](const Student& s) { return s.id == my_id; });

    if (fnd == v.begin()) {
        std::cout << "Xepa Champion" << std::endl;
    } else {
        std::cout << fnd - v.begin() + 1 << std::endl;
    }

    return 0;
}
```

#### F - 水王级魔法师

签到。

```cpp
#include <iostream>
#include <unordered_map>
#include <limits>
#include <cassert>
using i64 = long long;

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    std::unordered_map<int, i64> t;
    for (i64 i = 1, v = 2LL; v < i64(std::numeric_limits<int>::max()); ++i, v *= 2) {
        t[i] = v - 1LL;
    }

    int n;
    std::cin >> n;

    int ans = 0;
    while (n--) {
        int i;
        std::cin >> i;
        ans += static_cast<int>(t[i]);
        assert(ans >= 0);
    }

    std::cout << ans << std::endl;

    return 0;
}
```

#### G - 鸭鸭杯

暴力即可。

```cpp
#include <iostream>
#include <numeric>
using i64 = long long;
constexpr auto inf = 0x3f3f3f3f;

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    int t;
    std::cin >> t;
    while (t--) {
        int g, l, m;
        std::cin >> g >> l >> m;
        if (g < l) std::swap(g, l);
        if (g == l) {
            if (m % g == 0) {
                std::cout << m / g << std::endl;
            } else {
                std::cout << -1 << std::endl;
            }
            continue;
        }

        int ans = inf;
        for (int f = m / g + 1; f >= 0; --f) {
            auto remain = m - f * g;
            if (remain < 0) continue;
            if (remain % l == 0) {
                ans = f + remain / l;
                break;
            }
        }

        std::cout << (ans == inf ? -1 : ans) << std::endl;
    }

    return 0;
}
```

#### H - 龙族的传送魔法

BFS 模板。

```cpp
#include <iostream>
#include <queue>
#include <deque>
#include <utility>
#include <map>
using i64 = long long;
constexpr int dir[][2] = {1, 0, -1, 0, 0, 1, 0, -1};

int operator-(std::pair<int, int> b, std::pair<int, int> a) {
    return (b.first - a.first) + (b.second - a.second);
}

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    int w, h;
    std::cin >> w >> h;
    std::pair<int, int> start, end;
    std::cin >> start.first >> start.second >> end.first >> end.second;

    int cnt_portal;
    std::cin >> cnt_portal;
    std::map<std::pair<int, int>, std::pair<int, int>> portals;
    while (cnt_portal--) {
        int sx, sy, ex, ey;
        std::cin >> sx >> sy >> ex >> ey;
        portals[std::make_pair(sx, sy)] = std::make_pair(ex, ey);
    }

    std::vector vis(w, std::vector(h, false));
    std::deque<std::pair<int, int>> q;
    vis[start.first][start.second] = true;
    q.push_back(start);
    int depth = 0;
    bool is_reached = false;
    while (!q.empty()) {
        int s = q.size();

        while (s--) {
            auto fr = q.front();
            q.pop_front();
            if (fr == end) {
                is_reached = true;
                break;
            }

            for (int d = 0; d < 4; ++d) {
                int nxt_x = fr.first + dir[d][0], nxt_y = fr.second + dir[d][1];
                if (nxt_x < 0 || nxt_x >= w || nxt_y < 0 || nxt_y >= h || vis[nxt_x][nxt_y])
                    continue;
                vis[nxt_x][nxt_y] = true;
                q.push_back({nxt_x, nxt_y});
            }

            if (auto fnd = portals.find(fr); fnd != portals.end()) {
                vis[fnd->second.first][fnd->second.second] = true;
                q.push_back(fnd->second);
            }
        }
        if (is_reached) break;
        ++depth;
    }

    std::cout << (end - start) - depth << std::endl;

    return 0;
}
```

#### i - 黄金律法之谜

背包 DP。

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>
#include <limits>
using i64 = long long;
constexpr auto inf = std::numeric_limits<int>::max();

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    int r, n;
    std::cin >> r >> n;
    std::unordered_map<int, int> cnt_map;
    while (n--) {
        int cnt_rune, val_rune;
        std::cin >> cnt_rune >> val_rune;
        cnt_map[val_rune] += cnt_rune;
    }

    std::vector cnt(cnt_map.begin(), cnt_map.end());
    n = cnt.size();
    std::vector f(n + 1, std::vector(r + 1, 0));
    for (int i_rune = 1; i_rune <= n; ++i_rune) {
        for (int i_r = 1; i_r <= r; ++i_r) {
            f[i_rune][i_r] = inf;
            int rune_val = cnt[i_rune - 1].first;
            for (int c = 0; c <= cnt[i_rune - 1].second; ++c) {
                int i_rd = std::max(0, i_r - rune_val * c);
                if (f[i_rune - 1][i_rd] == inf) continue;
                int acc = f[i_rune - 1][i_rd] + rune_val * c;
                if (acc >= i_r) {
                    f[i_rune][i_r] = std::min(f[i_rune][i_r], acc);
                }
            }
        }
    }

    std::cout << (f[n][r] == inf ? -1 : f[n][r]) << std::endl;

    return 0;
}
```

#### J - 开放世界

单源最短路模板。

```cpp
#include <iostream>
#include <vector>
#include <limits>
using i64 = long long;
constexpr i64 inf = 0x3f3f3f3f3f3f3f3fLL;

// https://oi-wiki.org/graph/shortest-path/#dijkstra-%E7%AE%97%E6%B3%95
struct edge {
    i64 v, w;
};

std::vector<std::vector<edge>> e;
std::vector<i64> dis, vis;

void dijkstra(int n, int s) {
    dis[s] = 0;
    for (int i = 1; i <= n; i++) {
        i64 u = 0, mind = inf;
        for (int j = 1; j <= n; j++)
            if (!vis[j] && dis[j] < mind) u = j, mind = dis[j];
        vis[u] = true;
        for (auto ed : e[u]) {
            i64 v = ed.v, w = ed.w;
            if (dis[v] > dis[u] + w) dis[v] = dis[u] + w;
        }
    }
}

int main()
{
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    int n, q;
    std::cin >> n >> q;
    e.resize(n + 1);
    dis.resize(n + 1, std::numeric_limits<i64>::max());
    vis.resize(n + 1);

    for (int i = 0; i < q; ++i) {
        int a, b, d;
        std::cin >> a >> b >> d;
        e[a].push_back({1LL * b, 1LL * d});
        e[b].push_back({1LL * a, 1LL * d});
    }

    dijkstra(n, 1);

    std::cout << (dis[n] == std::numeric_limits<i64>::max() ? -1 : dis[n]) << std::endl;

    return 0;
}
```

#### K - 画家算法

二维差分、前缀和。

```cpp
#include <iostream>
#include <vector>
using i64 = long long;

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    int w, h, n;
    std::cin >> w >> h >> n;
    std::vector diff(w + 2, std::vector(h + 2, 0));
    for (int i = 0; i < n; ++i) {
        int x1, y1, x2, y2;
        std::cin >> x1 >> y1 >> x2 >> y2;
        ++x1, ++y1, ++x2, ++y2;
        ++diff[x1][y1];
        --diff[x1][y2 + 1];
        --diff[x2 + 1][y1];
        ++diff[x2 + 1][y2 + 1];
    }
    for (int i = 1; i <= w; ++i) {
        for (int j = 1; j <= h; ++j) {
            diff[i][j] += diff[i - 1][j] + diff[i][j - 1] - diff[i - 1][j - 1];
        }
    }
    std::vector pref(w + 1, std::vector(h + 1, 0));
    for (int i = 1; i <= w; ++i) {
        for (int j = 1; j <= h; ++j) {
            pref[i][j] = diff[i][j] + pref[i - 1][j] + pref[i][j - 1] - pref[i - 1][j - 1];
        }
    }

    int q;
    std::cin >> q;
    while (q--) {
        int x1, y1, x2, y2;
        std::cin >> x1 >> y1 >> x2 >> y2;
        ++x2, ++y2;
        std::cout << pref[x2][y2] - pref[x1][y2] - pref[x2][y1] + pref[x1][y1] << std::endl;
    }

    return 0;
}
```

#### L - 本次比赛的白给题

读题题。模拟。

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <unordered_set>
#include <algorithm>
#include <set>
#include <cctype>
using i64 = long long;

int main() {
    std::ios::sync_with_stdio(false);
    std::cin.tie(nullptr);

    std::string token;
    std::vector<std::unordered_set<std::string>> params;
    std::vector<std::set<std::string>> vars;
    while (std::cin >> token) {
        if (token == "#") {
            params.push_back({});
            vars.push_back({});
            while (std::cin >> token) {
                if (token == ":") break;
                params.back().insert(token);
            }
        } else if (std::all_of(token.begin(), token.end(), islower)) {
            if (params.back().find(token) == params.back().end()) {
                vars.back().insert(token);
            }
        }
    }

    int n = vars.size();
    for (int i = 0; i < n; ++i) {
        std::cout << i + 1;
        for (auto var : vars[i]) {
            std::cout << ' ' << var;
        }
        std::cout << std::endl;
    }

    return 0;
}
```

### Python

#### A

```python
width = [0]
s = 0
UPPER_BOUND = 1 << 63
v = 1
while s <= UPPER_BOUND:
    width.append(v)
    s += v
    if len(width) % 2 == 0:
        v *= 2
    else:
        v *= 3

while True:
    try:
        n = int(input())
        s = 0
        for i, e in enumerate(width):
            s += e
            if n < s:
                break
        print(i, n - (s - width[i]) + 1)
    except EOFError:
        break
```

#### B

```python
n = int(input())
for _ in range(n):
    var = input()
    if not (var[0].isalpha() or var[0] == '_'):
        print("No")
        continue
    if any([not (c.isalnum() or c == '_') for c in var]):
        print("No")
        continue
    print("Yes")
```

#### C

```python
n = int(input())
seq = []

def print_seq(seq):
    if len(seq) == 0:
        print('empty')
        return
    print(','.join(seq))

for _ in range(n):
    instr = input().split()
    if instr[0] == 'q' or instr[0] == 's':
        seq.append(str(int(instr[1])))
    elif instr[0] == 'd':
        print_seq(seq)
    elif instr[0] == 'Q':
        if len(seq) != 0:
            seq.pop(0)
    elif instr[0] == 'S':
        if len(seq) != 0:
            seq.pop()
```

#### D

```python
s = input()
n = len(s)
REV = {'r': 'o', 'o': 'r', 'x': 'y', 'y': 'x'}
cnt = [0, 0]

def update(c):
    global cnt
    if c == 'r':
        cnt[0] += 1
    elif c == 'o':
        cnt[0] -= 1
    elif c == 'x':
        cnt[1] += 1
    elif c == 'y':
        cnt[1] -= 1
def check():
    return cnt[0] == 0 and cnt[1] == 0

ans = 0
for d in range(2, n):
    cnt = [0, 0]
    for i in range(d):
        update(s[i])
    if check():
        ans = d
        continue
    for i in range(d, n):
        update(REV[s[i - d]])
        update(s[i])
        if check():
            ans = d
            break

print(ans)
```

#### E

```python
my_id = int(input())
ids = list(map(int, input().split()))
pps = list(map(int, input().split()))
sps = list(map(int, input().split()))

class Player:
    def __init__(self, pid, pp, sp):
        self.pid = pid
        self.pp = pp
        self.sp = sp
        self.rp = 2 * pp + 1 * sp

players = []
for i in range(len(ids)):
    players.append(Player(ids[i], pps[i], sps[i]))
players.sort(key=lambda p : (-p.rp, -p.pp, -p.sp, p.pid))

for i, player in enumerate(players):
    if player.pid == my_id:
        if i == 0:
            print("Xepa Champion")
        else:
            print(i + 1)
```

#### F

```python
m = [0]
s = 2
UPPER_BOUND = 1 << 32
while s <= UPPER_BOUND:
    m.append(s - 1)
    s *= 2

n = int(input())
ans = 0
for _ in range(n):
    t = int(input())
    ans += m[t]
print(ans)
```

#### G

```python
from math import inf

t = int(input())
for _ in range(t):
    a, b, m = list(map(int, input().split()))
    if a < b:
        a, b = b, a
    elif a == b:
        if m % a == 0:
            print(m // a)
        else:
            print(-1)
        continue

    ans = inf
    for f in range(m // a + 1, -1, -1):
        remain = m - f * a
        if remain < 0: continue
        if remain % b == 0:
            ans = f + remain // b
            break

    print(ans if ans != inf else -1)
```

#### H

```python
w, h, ax, ay, bx, by = list(map(int, input().split()))
t = int(input())
portals = dict()
for _ in range(t):
    x1, y1, x2, y2 = list(map(int, input().split()))
    portals[(x1, y1)] = (x2, y2)

DIR = [(1, 0), (-1, 0), (0, 1), (0, -1)]
q = []
q.append((ax, ay))
vis = [[False] * h for _ in range(w)]
vis[ax][ay] = True
depth = 0
is_reached = False
while len(q) != 0:
    s = len(q)
    for _ in range(s):
        curr = q[0]
        q.pop(0)
        if curr[0] == bx and curr[1] == by:
            is_reached = True
            break

        for d in DIR:
            nxt_x, nxt_y = curr[0] + d[0], curr[1] + d[1]
            if nxt_x < 0 or nxt_x >= w or nxt_y < 0 or nxt_y >= h or vis[nxt_x][nxt_y]:
                continue
            vis[nxt_x][nxt_y] = True
            q.append((nxt_x, nxt_y))

        if curr in portals:
            dest = portals[curr]
            q.append(dest)
            vis[dest[0]][dest[1]] = True

    if is_reached: break
    depth += 1

print(abs(ax - bx) + abs(ay - by) - depth)
```

#### L

```python
tokens = input().split()
func_env = []
captured = []

is_parsing_params = False
for token in tokens:
    if is_parsing_params:
        if token == ":":
            is_parsing_params = False
            continue
        func_env[-1].add(token)
    if token == "#":
        func_env.append(set())
        captured.append(set())
        is_parsing_params = True
        continue
    elif all([c.isalpha() for c in token]):
        if not token in func_env[-1]:
            captured[-1].add(token)

for i, c in enumerate(captured):
    print(i + 1, end='')
    c = sorted(list(c))
    for name in c:
        print(' ' + name, end='')
    print()
```

## Ereflect

### Python

#### B

```py
def check_string(s):
    digits = [str(x) for x in range(10)]
    chars = [chr(x) for x in range(95) if x != 32]
    if s[0] in digits:
        return 'No'
    if any(c not in set(chars + digits) for c in s):
        return 'No'
    return 'Yes'

n = int(input())
for _ in range(n):
    s = input().strip()
    ans = check_string(s)
    print(ans)
```

#### C

```py
def list_operation(commands):
    l = []
    for cmd in commands:
        if cmd[0] == 'q' or cmd[0] == 's':
            l.append(int(cmd[1]))
        elif cmd[0] == 'S' and l:
            l.pop()
        elif cmd[0] == 'Q' and l:
            l = l[1:]
        elif cmd[0] == 'd':
            if not l:
                print("empty")
                continue
            print(','.join(str(i) for i in l))
    return l

n = int(input())
commands = [input().split() for _ in range(n)]
list_operation(commands)
```

#### F

```py
n = int(input())
l = [int(input()) for _ in range(n)]
maxx = max(l)
mapl = [2 ** (i - 1) for i in range(1, maxx + 2)]
mapl[1:] = [mapl[i - 1] + mapl[i] for i in range(1, maxx + 1)]
ans = sum(mapl[i - 1] for i in l)
print(ans)
```
