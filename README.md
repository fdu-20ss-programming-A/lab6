# Lab 6

> 本次lab目标：
>
> 1. 回顾上次Lab5作业
> 2. 利用数组特性解决问题



## 获取及提交Lab

**获取**：通过 `https://github.com/fdu-20ss-programming-A/lab6`或者`超星平台`获取。

**提交**：超星平台上已经发布了LAB6作业，同学需要将每题的**代码**、**运行结果**、个人对题目的思考体会（可选）以**图片**或者**文档**（ word 或者 pdf ）的形式在超星LAB6对应的作业区域提交即可。

**提交物**：代码、运行结果，每题可整理为一份 word 或者 pdf 文档，也可以将两者截在一张图片上提交。

**截止时间**：2020年11月10日 23:59:59



## 1. Lab 5回顾

> LAB 5复习了多重循环相关知识

### 循环

#### 三种循环

```c
while(condition)
{
   statement(s);
}
```

```c
for ( init; condition; increment )
{
   statement(s);
}
```

```c
do
{
   statement(s);

}while( condition );
```

#### 多重循环/嵌套循环

```C
for (initialization; condition; increment/decrement)
{
    statement(s);
    for (initialization; condition; increment/decrement)
    {
        statement(s);
        ... ... ...
    }
    ... ... ...
}
```

### 循环控制语句


| 控制语句                                                     | 描述                                                         |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [break 语句](https://www.runoob.com/cprogramming/c-break-statement.html) | 终止**循环**或 **switch** 语句，程序流将继续执行紧接着循环或 switch 的下一条语句。 |
| [continue 语句](https://www.runoob.com/cprogramming/c-continue-statement.html) | 告诉一个循环体立刻停止本次循环迭代，重新开始下次循环迭代。   |

### 循环应用



## 2. Lab 5作业讲解

### 第一题

题目

> 编写一个程序，显示从101年到2100年的所有闰年
>
> 每行10个，用空格分隔

提示
> 闰年分为普通闰年和世纪闰年
>
> 公历年份是4的倍数的，且不是100的倍数，为普通闰年（如2004年、2020年就是闰年）
>
> 公历年份是整百数的，必须是400的倍数才是世纪闰年（如1900年不是世纪闰年，2000年是世纪
> 闰年）


参考答案：

```C
#include <stdio.h>
#include <stdlib.h>
int main(){
	printf("All the leap years from 101 to 2100:\n");
	int count = 0;
	for (int year = 101; year <= 2100; year++){
		if ((year % 4 == 0 && year % 100 != 0) || year % 400 == 0){
			count++;
			if(count % 10 == 0){
				printf("%d\n", year);
			}else{
				printf("%d ", year);
			}
		}
	}
    return 0;
}
```

补充：
```text
十位换行选择用year计算有没有到10当然也行
```



### 第二题

题目

> 编写一个程序，提示用户输入一个十进制自然数并显示其对应的二进制值

示例

> 请输入一个十进制自然数：100
>
> 十进制数“100”的二进制值为：1100100

出现的问题：

```c
1. 直接调库
```

参考答案：

```C
#include <stdio.h>
#include <stdlib.h>
int main(){
	printf("请输入一个十进制自然数：");
	int decimal;
	int result[20];
	int index = 0;
	scanf("%d", &decimal);
	for (int i = decimal; i > 0; i /= 2){
		result[index++] = i % 2;
	}
	printf("十进制数“%d”的二进制值为：", decimal);
	for(int i = index - 1; i >= 0; i--){
		printf("%d ", result[i]);
	}
	return 0;
}
```

额外知识点：

```text
利用scanf返回值检查输入正确性
https://blog.csdn.net/HNAKXR/article/details/81046708
```


### 第三题

题目

> 使用如下式子来近似e：
>
> e = 1 + $\frac{1}{1!}$ + $\frac{1}{2!}$ + $\frac{1}{3!}$ + $\frac{1}{4!}$ + ... + $\frac{1}{i!}$  
>
> 编写一个程序，显示i = 1, 2, 3, ...., 10时的e值
>
> 保留20位小数

示例

> i = 1时，e值为 2.00000000000000000000
> 
> i = 2时，e值为 2.50000000000000000000
> 
> i = 3时，e值为 2.66666666666666650000
> 
> i = 4时，e值为 2.70833333333333300000
> 
> i = 5时，e值为 2.71666666666666630000
> 
> i = 6时，e值为 2.71805555555555540000
> 
> i = 7时，e值为 2.71825396825396840000
> 
> i = 8时，e值为 2.71827876984127000000
> 
> i = 9时，e值为 2.71828152557319220000
> 
> i = 10时，e值为 2.71828180114638450000

参考答案：

```C
#include <stdio.h>
#include <stdlib.h>
int main(){
	double e;
	for (int value = 1; value <= 10; value++){
		e = 1.0;
		for (int i = 1; i <= value; i++){
			double denominator = i;
			for (int k = i - 1; k >= 1; k--){
				denominator *= k;
			}
			e += 1 / denominator;
		}
		printf("i = %d时，e值为 %.20lf\n", value, e);
	}
    return 0;
}
```

补充：
```text
阶乘计算的循环可以用运用数学知识进行简化。
```


### 第四题

题目

> 编写一个程序，提示用户输入一个年份和该年第一天是星期几这两个信息，然后输出该年中每个
> 月的第一天是星期几
>
> 输入时依次用1~7代表星期一到星期日

出现的问题
```c
代码重复，对闰年的处理
```

参考答案：

```C
#include <stdio.h>
#include <stdlib.h>
int main(){
	printf("请输入年份与星期几：");
	int year, day;
	scanf("%d,%d", &year, &day);
	for(int month = 1; month <= 12; month++){
		printf("%d年%d月1日是星期", year, month);
		day %= 7;
        switch(day){
            case 0:
                printf("日\n");
                break;
            case 1:
                printf("一\n");
                break;
            case 2:
                printf("二\n");
                break;
            case 3:
                printf("三\n");
                break;
            case 4:
                printf("四\n");
                break;
            case 5:
                printf("五\n");
                break;
            case 6:
                printf("六\n");
                break;
		}
        if(month == 2){
            if((year % 4 == 0 && year % 100 != 0) || year % 400 == 0){
            	day += 29;
            }else{
            	day += 28;
            }
        }else if(month == 4 || month == 6 || month == 9 || month == 11){
            day += 30;
        }else{
            day += 31;
        }
    }
    return 0;
}
```

补充：
```text
1. 日期打印可以用数组进行简化
2. month的判断可以用switch case 代替
```




## 3. Lab 6上机作业

> 本次作业考察数组基础应用。

### 数组

#### 声明数组

在 C 中要声明一个数组，需要指定元素的类型和元素的数量，如下所示：

```
type arrayName [ arraySize ];
```
#### 初始化数组

```C
double balance[] = {1000.0, 2.0, 3.4, 7.0, 50.0};
balance[4] = 50.0;
```

#### 数组操作

```C
int n[10] = 0; 
n[9] = 5;
```

#### 数组访问

```C
double salary = balance[9];
int n[ 10 ] = 0;
for (j = 0; j < 10; j++ ) {
    printf("Element[%d] = %d\n", j, n[j] );
}
```

### Question 1

题目

> 编写一个程序，先输入数字数量，然后输入具体数据，给出这组数据中的最大元素和次最大元素以及他们相应的序号（序号从0开始，默认数据各不相同）。
>
> 最多10个数字
> 要求：请先选择合适的数据结构存储数据，再对数据进行比较操作。本次默认输入都合法。

输出示例

> 请输入个数：8
>
> 输入具体数据：1，2，5，6，0，3，4，9
> 
> 输出：最大元素：9  序号为7        次最大元素：6 序号为3

### Question 2

题目

> 编写一个程序，先输入每行数字的数量和数据总数，然后输入具体的数据（数据为0~3之间的整数），按照0对应A，1对应B，2对应C，3对应D的规则，分行打印出映射后的图案。
>
> 最多50个数字

示例：

> 请输入每行数量和数据总数：5 20
>
> 输入数据： 1 1 1 1 1 1 0 2 0 1 1 0 3 0 1 1 1 1 1 1
>
> 输出：
>
> B B B B B
>
> B A C A B
>
> B A D A B
>
> B B B B B
>
> 要求先选择合适的数据结构存储下面结构，默认输入都合法。
>
> 注：可以使用一维数组或者二维数组存储结构。

### Question 3

题目

> 有n个人围成一圈,顺序排号，从第一个开始报数(从1到3报数)，凡报到3的人退出圈子，问最后留下的是原来第几号的那位。
>
> 最多40个人

输出示例

> 输入n: 3
>
> 最后留下的是：2

### Question 4 学习反馈
> 课程已经过半，期中考试就要来来，请同学们描述一下现在自己的学习状态和困扰帮助我们更好改进我们的课程吧！
> 
> 角度可以是：每周学习本门课程所用的时间大概是多少？和其它课相比占用的时间多吗？ 上课听讲感受如何？能跟得上吗？ 课后作业自己独立完成有困难吗？ 整体而言感觉这门课难吗？如果难的话，困难的点在哪里呢？
