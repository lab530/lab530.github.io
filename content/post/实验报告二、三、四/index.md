+++
slug = "Experiment report two, three and four"
title = '实验报告二、三、四'
date = 2024-09-09T23:49:57+08:00
weight=7

categories = [
    "实验报告"
]


+++

输入a，b，c，编程求方程 ax2 + bx + c = 0 的根。
```c
#include<stdio.h>
#include<math.h>
int main()
{
	int d;  //  
	double a, b, c;
	scanf("%lf %lf %lf", &a, &b, &c);
	double data = b * b - 4 * a * c;
	if(data >= 0)
	{
		if(data == 0)
		{
			printf("该方程的根为： %lf",((-b + sqrt(data)) / -2 * a));	
		}
		else
		{
			printf("该方程有两个跟: %lf %lf",((-b + sqrt(data)) / -2 * a),((-b - sqrt(data))/ -2 * a));
		}
	}
	else
	{
		printf("该方程无解!");
	}
	return 0;
}
```

已知正方体的棱长为 3.2，求正方体的体积和表面积 （保留 2 位小数）。
```c
#include<stdio.h>
#include<math.h>
int main()
{
	double a = 3.2;
	printf("该正方体的体积为:%.2lf\n", pow(a, 3));
	printf("该正方体的表面积为:%.2lf\n", 6 * pow(a, 2));
	return 0;
}
```


输入3个整数a、b、c，编程交换他们的值，即把 a 的值给 b ，b 的值给 c ， c 的值给 a 。
```c
#include <stdio.h>
int main( )
{	
    int a, b, c, t;
    scanf("%d %d %d", &a, &b, &c);
    t=c;
    c=b;
    b=a;
    a=t;
    printf("a=%d b=%d c=%d", a, b, c);
    return 0;
}
```

编程将任意输入的小写字母转化成大写字母并输入（要求使用 getchar 和 putchar 函数完成）。
```c
#include<stdio.h>
#include<math.h>
int main()
{
	int a;
	a = getchar();
	putchar(a - ('a' - 'A'));
	return 0;
}
```

输入三角形的三条边，编程求该三角形的面积。
```c
#include <stdio.h>
#include <math.h>
int main( )
{	
    // 缺少判断三角形是否合理
    float a,b,c,p,s;
    scanf("%f %f %f", &a, &b, &c);
    p = (a + b + c) / 2;
    s=sqrt((p - c) * (p - a) * (p - b) * p);
    printf("该三角形的面积是：%.2f", s);
    return 0;
}
```

设计一个简单的计算器程序，用户输入运算数和四则运算符，输出计算的结果(请注意处理当输入除数为 0 的错误提示)。示范如下：
输入:5.8*6
输出:5.8*6=34.8
输入：9/0
输出：error！除数不能为0！
```c
#include<stdio.h>
#include<math.h>
int main()
{
	double a, b;
	char c;
	scanf("%lf%c%lf", &a, &c, &b);
	switch(c)
	{
		case '+':
			printf("%lg%c%lg=%lg\n", a, c, b, a + b);
			break;				
		case '-':
			printf("%lg%c%lg=%lg\n", a, c, b, a - b);
			break;
		case '*':
			printf("%lg%c%lg=%lg\n", a, c, b, a * b);
			break;
		case '/':
			if(b == 0)
			{
				printf("error!");
			}
			else
			{
				printf("%lg%c%lg=%lg\n", a, c, b, a / b);
			}
			break;
	}	
	return 0;
}
```

根据输入的 x 的值求 y 的值，当 x 大于 0 时，y =（x + 1）/（x - 2）；当 x 等于 0 或 2 时，y = 0；当 x 小于 0 时，y =（x - 1）/（x - 2）。（注意测试 x 为 2 时程序能否正确执行）
```c
#include <stdio.h>                                   
int  main()
{   
	float x;
	scanf("%f",&x);
	if (x == 0 || x == 2)printf("y=%d\n",0);
	else 
	{
		if(x > 0)printf("y=%.2f\n", (x + 1) / (x - 2));
		if(x < 0)printf("y=%.2f\n",(x - 1) / (x - 2));
	}
	return 0;
}
```

编写程序，输入一个不多于 4 位的正整数，完成下列要求：
○1 判断它是几位数，如输入 152，输出 3
○2 输出每一位的数码，如输入 152，输出 1, 5, 2
○3 逆序输出这个数，如输入 152，输出 251
输入示例: 152
输出: 152 是 3 位数, 数码是1、5、2，逆序数字是 251
```c
#include <stdio.h>  
#include <math.h>                             
int  main()
{   
	int a, b, c, i = 0;
	scanf("%d",&a);
	b = a;
	for(i = 1; a >= 10; i++)
	{
		a /= 10;
		c = i + 1; 
	}
	printf("%d是%d位数,",b,i);
		int sum=0;
	for (; c >= 0; c--)
	{	
		sum += (b % 10) * pow(10 ,c - 1);
		b /= 10;
	
	}
	c = sum;
	printf("数码是") ;
	while(i > 0)
	{	
		if (sum > 10) printf("%d、", sum % 10);
		else printf("%d,", sum % 10);
		sum /= 10;
		i--;
	}
	printf("逆序数是%d",c); 
	return 0;
}
```

选做题）用 switch 结构编程完成：输入月份数字，输出对应的季节，12 - 2 月是冬季，3 - 5 月是春季，6 - 8 月是夏季，9 - 11 月是秋季。（最好不写 12 个 case 语句，这题是可以用 4 个 case 解决的）
```c
#include <stdio.h>  // 数据合理的情况下
int main()
{
	int a,b;
	scanf("%d",&a);
	b = a / 3;
	switch(b)
	{
		case 1:
			printf("春季");
			break;
		case 2:
			printf("夏季");
			break;
		case 3:
			printf("秋季");
			break;
		default:
			printf("冬季");
	}
	return 0; 
}
```

鸡兔同笼：35 个头，94 只脚，问鸡、兔各多少只？(答案，鸡 23 兔 12)
```c
#include<stdio.h>
int main()
{	int head, foot, chicken = 0, rabbit = 0;
	printf("请输入头和腿的数量，并用空格隔开:\n");
	scanf("%d %d", &head, &foot);
	for (chicken=0; chicken <= head; chicken++)
	{
		for (rabbit=0; rabbit <= head; rabbit++)
		{	
			if(rabbit + chicken == head && rabbit * 4 + chicken * 2 == foot)
			printf("鸡的数量为：%d只，兔的数量为：%d只\n", chicken, rabbit);
		}
		
	}
	return 0 ;
}
```

计算 1 ~ 100 以内所有含 6 的数的和。
```c
#include<stdio.h>
int main()
{	int sum = 0;
	for (int i = 0; i <= 100; i++)
	{
		if(i % 6 == 0 || i / 10 == 6 || i % 10 == 6)
		    sum += i;		
	}
	printf("%d", sum);
	return 0 ;
}
```

求数列 2 / 1，3 / 2，5 / 3，8 / 5，13 / 8 … 前 20 项之和。（答案，32.660259）
```c
#include<stdio.h>
int main()
{	float sum=0, a, b, count = 1;
	for(float a = 2; count <= 20; count++)
	{
		for (float b = 1; count <= 20; count++)
		{
			sum += a / b;
			a += b;
			b = a - b;
		}
		printf("%f", sum);	
	}	
	return 0 ;
}
```

验证谷角猜想。日本数学家谷角静夫在研究自然数时发现了一个奇怪现象：对于任意一个自然数 n ，若 n 为偶数，则将其除以 2 ；若 n 为奇数，则将其乘以 3 ，然后再加 1。如此经过有限次运算后，总可以得到自然数 1。人们把谷角静夫的这一发现叫做“谷角猜想”。
要求：编写一个程序，由键盘输入一个自然数 n ，把 n 经过有限次运算后，最终变成自然数 1 的全过程打印出来。
```c
#include<stdio.h>
int main()
{	int n;
	scanf("%d", &n);
	while(n != 1)
	{
		if(n % 2 == 1)
		{	
			n = n * 3 + 1;
			printf("(n*3)");
		}
		else
		{	
			n /= 2;
			printf("(n/2)");
		}
	}
	printf("=%d",n);	
	return 0 ;
}
```

编程输出课本 P161 页编程题第 6 题的图形。
```c
#include<stdio.h>
int main()
{
	int n = 7;
	for (int i = 1; i <= (n+1)/2; i++)
	{
			for (int b= 1; b <= n-(2*i-1); b++)
			{
				printf(" ");
			}
			for (int d = 0; d < 2 * i - 1; d++)
			{
				printf("* ");
			}
		printf("\n");
	}
	for (int i = (n - 1) / 2; i >=1; i--)
	{
		for (int b = 1; b <= n - (2 * i - 1); b++)
		{
			printf(" ");
		}
		for (int d = 0; d < 2 * i - 1; d++)
		{
			printf("* ");
		}
		printf("\n");
	}
	return 0;
}
```

从键盘输入 6 名学生的 5 门课成绩，分别统计每个学生的平均成绩（不用数组处理）。
```c
#include<stdio.h>
int main()
{	int count = 0;
	printf("请输入六名学生的五门成绩，分别用空格隔开：\n");
	while(count != 6)
	{	int sum = 0, grade = 0;
		float average = 0;
		for(int i = 1 ; i <= 5; i++)
		{
			scanf("%d", &grade);
			sum += grade;
		}
		average = sum / 5;
		printf("该学生的平均成绩为：%.2f\n", average);
		count ++;
	}
	return 0 ;
}
```

打印乘法口诀表。
```c
#include <stdio.h>

int main(void)
{
    int i, j;
    for (i = 1; i <= 9; i++) {
        for (j = 1; j <= i; j++) {
            printf("%dx%d=%2d ", j, i, j * i);
        }
        printf("\n");
    }
} 
```