+++
slug = "2022-NewRound1"
title = '2022 - NewRound1'
date = 2024-09-09T23:49:57+08:00
weight=6

categories = [
    "题解"
]


+++

A - 任何伟大的目标，都离不开微不足道的开始

```c
#include <stdio.h>
int main(){
    printf("Hello world!");
    return 0;
}
```

B - D 换下运算符

```c
#include <stdio.h>
int main(){
    int a, b;
    scanf("%d %d", &a, &b);
    printf("%d", a + b);// C 改成 a - b, D 改成 a * b
    return 0;
}
```

E - A / B

```c
#include <stdio.h>
int main(){
    double a, b;
    double c;
    scanf("%lf %lf", &a, &b);
    if(b == 0)  printf("False");
    if(b != 0) {
        c = a / b;
        printf("%.2lf", c);
    }
    return 0;
}
```
F - 判断成绩
```c
#include <stdio.h>
int main(){
    int i;
    scanf("%d", &i);
    if(i > 100){
        printf("False!");
    }else if(i >= 90){
        printf("A");
    }else if(i >= 80){
        printf("B");
    }else if(i >= 70){
        printf("C");
    }else if(i >= 60){
        printf("D");
    }else if(i >= 0){
        printf("E");
    }else{
        printf("False!");
    }
    return 0;
}
```
G - 求三角形面积

```c
#include <stdio.h>
#include <math.h>
int  main(){
  double  a, b, c, p, s;
  scanf ( "%lf %lf %lf", &a, &b, &c);
  if (a + b > c && a + c > b && b + c > a)
  {
    p = (a + b + c) / 2;
    s = sqrt(p * (p - a) * (p - b) * (p - c));
    printf ( "%.2lf\n", s);
  }
  else  printf ("Fail\n");
  return  0;
}
```

H - 间距

```c
#include <stdio.h>
#include <math.h>
int main(){
    float d;
    int x1, y1, x2, y2;
    scanf("%d %d %d %d", &x1, &y1, &x2, &y2);
    d = sqrt((float)(x2 - x1) * (x2 - x1) + (y2 - y1) * (y2 - y1));
    printf("%.2lf", d);
    return 0;
}
```
I - 求绝对值
```c
#include <stdio.h>
#include <math.h>
int main(){
    float a;
    scanf("%f", &a);
    printf("%.2f", fabs(a));
    return 0;
}
```
J - 明明买文具
```c
#include <stdio.h>
int main() {
	double a;
	double b;
	scanf("%lf %lf", &a, &b);
	printf("%d", (int)((a + b / 10) / 1.5));
	return 0;
}
```

