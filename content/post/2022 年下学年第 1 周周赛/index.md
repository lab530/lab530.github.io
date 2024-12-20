+++
slug = "Week 1 of the next school year 2022"
title = '2022 年下学年第 1 周周赛'
date = 2024-09-09T23:49:57+08:00
weight=6

categories = [
    "题解"
]


+++

A.cpp

基本思路：一个个写例发现是个循环群，不断的取构造 3的倍数来计算循环群所对应的结果。

```cpp
#include<iostream>
using namespace std;
int n, ans, a;
int main()
{
	cin >> n;
	while(n--)
	{
		cin >> a;
		ans = 1e9 + 1;
		if(a % 3)
		{
			for(int i = -2; i < 3; i++)
				if((a-i*2) % 3 == 0)
					ans = min(ans,abs((a-i*2)/3) + abs(i));
		}
		else ans = a / 3;
		cout << ans << endl; 
	}
	return 0;
}
```

B.cpp

基本思路：对于新读入的一个数，判断最小的位置是否改变，若没有改变就改变，若已改变就查 m+1-ai

```cpp
#include <iostream>
#include <string>
using namespace std;
 
int main()
{
    int t;
    cin >> t;
    while (t--) {
        int m, n;
        cin >> m >> n;
        string cons(n, 'B');
        while (m--) {
            int k;
            cin >> k;
            k--;
            if (k >= n / 2) {
                k = n - 1 - k;
            }
            if (cons[k] == 'B') {
                cons[k] = 'A';
            } else if (cons[n - 1 - k] == 'B') {
                cons[n - 1 - k] = 'A';
            }
        }
        cout << cons << endl;
    }
    return 0;
}
```

C.cpp

基本思路：水题，主要是 CNN 准确率计算，对于一个矩阵来说，需要计算正确元素的个数 / 总元素的个数。

```cpp
#include<iostream>
#include<string>
using namespace std;
int m;
double correct = 0, n = 0;
string a,b,c;
void judge(string a, string b)
{
	for(int i = 0; i < a.length(); i++)
		if(a[i] != b[i]) return;
	correct++;
}
int main()
{
	cin >> n >> m;
	getline(cin, c);
	for(int i = 0; i < n; i++)
	{
		getline(cin, a);
		getline(cin, b);
		judge(a, b);	
	}
	printf("%.2lf%%\n", correct/n*100);
	return 0;
}
```

D.cpp

基本思路： 此处尽可能大是讲日期尽可能的分成二等段即 `abs(l1 - l2) ` 和 `abs(l2 - l3)` 差最小的时候。

```cpp
#include <iostream>
using namespace std;
 
int main()
{
    int t;
    cin >> t;
    while (t--) {
        int n;
        cin >> n;
        n -= 4;
        int ans;
        switch (n % 3) {
            case 0: case 1:
                ans = n / 3 - 1;
                break;
            default:   // 2
                ans = n / 3;
                break;
        }
        cout << ans << endl;
    }
    return 0;
}
```

E.cpp

基本思路：仔细想想，如果有 1 的话，左右两边合并成什么都不重要了，我只要保证最后一次合并有个 1 存在就行，而且题目限制 k <= n. 所以如果有 1 的话，总可以成功。

```cpp
#include<iostream>
using namespace std;
int t, n, k, a, num;
int main()
{
	cin >> t;
	while(t--)
	{
		cin >> n >> k;
		num = 0;
		for(int i = 0 ; i < n; i++)
		{
			cin >> a;
			if(a == 1) num++;
		}
		if(num == 0)	cout << "NO" << endl;
		else	cout << "YES" << endl;
	}
	return 0;
}
```

F.cpp

基本思路： 模拟水题，对于回文日期，直接从年份开始++，然后倒序复制到月份和日上，剩下的判断日期是否合理就行，对于这种解法，需要考虑 20200101 这类日期。

```cpp
#include <iostream>
using namespace std;
char arr[8];
int data[8];
int md[12] = {31,29,31,30,31,30,31,31,30,31,30,31};
bool flag1 = 1, flag2 = 1;
void solve()
{
    while(1)
    {
      data[3] ++;
      if(data[3] == 10)
      {
        data[2]++;
        data[3] = 0;
      }
      if(data[2] == 10) 
      {
        data[1]++;
        data[2] = 0;
      }
      if(data[1] == 10)
      {
        data[0]++;
        data[1] = 0;
      }
      int year = 0;
      for(int i = 0; i < 4; i++)
      {
        data[7-i] = data[i];
        year = year * 10 + data[i];
      }
      int month = data[4] * 10 + data[5];
      int day = data[6] * 10 + data[7];
      if(year % 400) md[1] = 28;
      else md[1] = 29;
      if(month > 12 || md[month - 1] < day) continue;
      if(flag1 || flag2)
      {
        if(flag1)
        {
          for(int i = 0; i < 8; i++)
            cout << data[i] ;
          cout << endl;
          flag1 = 0;
        }
        if(flag2)
        {
          if(data[0] == data[2] && data[1] == data[3] && data[1] != data[2])
          {
             for(int i = 0; i < 8; i++)
              cout << data[i] ;
            cout << endl;
            flag2 = 0;
          }
        }
      }
      if(!flag1 && !flag2) break;
    }
}
int main()
{
  for(int i = 0; i < 8; i++)
  {
    cin >> arr[i];
    data[i] = arr[i] - '0';
  }
  for(int i = 3; i >= 0 ;i--)
  {
      if(data[i] > data[7 - i])
      {
          data[3]--;
          break;    
      }
  }
  solve();
  return 0;
}
```
F.c
```c
#include<stdio.h>
int Ahuiwendate(int n) {
  while (n) {
    n++;
    int year = n / 10000;
    int day = n % 100;
    int month = (n % 10000) / 100;
    int uday = (day % 10) * 10 + day / 10;
    int umonth = (month % 10) * 10 + month / 10;
    if (year / 100 == uday && day < 31 && day > 0 && year % 100 == umonth && month < 13 && month > 0) {
      break;
    }
  }
  return n;
}
int Bhuiwendate(int n)
{
  while (n)
  {
    n++;
    int year = n / 10000;
    int day = n % 100;
    int month = (n % 10000) / 100;
    int uday = (day % 10) * 10 + day / 10;
    int umonth = (month % 10) * 10 + month / 10;
    if (day == month && year / 100 == uday && day < 31 && day > 0 && year % 100 == umonth && month < 13 && month > 0)
    {
      break;
    }
  }
  return n;
}
int main()
{
  int n;
  scanf("%d", &n);
  int x = Ahuiwendate(n);
  printf("%d\n", x);
  int y = Bhuiwendate(n);
  printf("%d\n", y);
  return 0;
}
```