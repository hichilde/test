## 一、数组

### 1.一维数组

##### 1.1一维数组的定义和初始化

1.定义一维数组

```c
type-t arr-name[const-n];
//type-t是指数组类型,arr-name为数组名称,const-n为常量表达式,指定数组大小
```

例如:

```c
eg1:
int arra[3];
eg2:
char arrb[3];
```

2.初始化

- 可以是完全初始化,也可以是不完全初始化


```c
//完全初始化(给所有元素赋值)
int arr1[5]={1,2,3,4,5};
//不完全初始化(给部分元素赋值)
int arr2[5]={1,2,3};
//如果不给元素赋值,大括号内要写0,不能不写
```

 元素不能超过数组指定长度

 如果已经赋值,也可以不指定数组长度,因为此时的数组已经有了确定的长度

- 还可以手动从键盘输入对数组初始化


```c
#include<stdio.h>
int main()
{
    int arr1[5]={0};
    int i=0;
    for(i=0;i<5;i++)
    {
        scanf("%d",&arr1[i]);
    }
    for(i=0;i<5;i++)
    {
        printf("%d ",arr1[i]);
    }
    return 0;
}
```

注意:数组下标从0开始,如果是a[3],则数组分别为a[0],a[1],a[2]

##### 1.2一维数组的使用

数组可以作为函数参数,数组名作实参实际上是将数组的首地址传给被调函数

```c
#include<stdio.h>
#define N 10
//输入学生分数,编程计算总分
void Readscore(int score[],int n);
int Sum(int score[],int n);
int main()
{
    int score[N],n,sum;
    printf("Input n:");
    scanf("%d",&n);
    Readscore(score,n);//数组名作为实参调用函数Readscore()
    sum=Sum(score,n);//数组名作为实参调用函数Sum()
    printf("sum score is %d\n",sum);
    return 0;
}
void Readscore(int score[],int n)//定义Readscore()函数
{
    int i;
    printf("Input score:");
    for(i=0;i<n;i++)
    {
        scanf("%d",&score[i]);
    }
}
int Sum(int score[],int n)//定义Sum()函数
{
    int i,sum=0;
    for(i=0;i<n;i++)
    {
        sum+=score[i];
    }
    return sum;
}
```

### 2.二维数组

##### 2.1.二维数组的定义和初始化

1.定义二维数组

```c
type-t arr-name[const-n1][const-n2];
//type-t是数组类型,arr-name是数组名,const-n1代表每一列元素个数,const-n2代表每一行元素个数
```

例如:

```c
int arr[3][4];
```

2.初始化

- 二维数组的初始化与一维数组初始化大致相同

```c
int arr1[3][4]={1,2,3,4,5,6,7,8,9,10,11,12};//按元素初始化
int arr2[3][4]={{1,2,3},{4,5,6},{7,8,9},{10,11,12}};//按行初始化
int arr[][4]={1,2,3,4,5,6,7,8,9,10,11,12};//二维数组的第一维长度声明可以省略,第二维不能
```

- 从键盘输入

```c
#include<stdio.h>
int main()
{
    int i,j;
    int arr[3][4];
    for(i=0;i<3;i++)
    {
        for(j=0;j<4;j++)
        {
            scanf("%d",&arr[i][j]);
        }
    }
    for(i=0;i<3;i++)
    {
        for(j=0;j<4;j++)
        {
            printf("%d ",arr[i][j]);
        }
    }
    return 0;
}
```

##### 2.2二维数组的使用

​       当形参被声明为一维数组时,形参列表中数组的方括号内可以为空,当形参被声明为二维数组时,可以省略第一维数组的长度声明,但不能省略第二维的长度声明

例如:

```c
//从键盘输入一个二维数组的元素值
//调用一个自定义函数求二维数组元素中最小值
#include<stdio.h>
#define M 3
#define N 4
int fun(int a[][N]);
int main()
{
    int b[M][N],i,j,min;
    for(i=0;i<M;i++)
    {
        for(j=0;j<N;j++)
            scanf("%d",&b[i][j]);
    }
    min=fun(b);
    printf("min=%d",min);
    return 0;
}
int fun(int a[][N])
{
    int i,j,min;
    min=a[0][0];
    for(i=0;i<M;i++)
    {
        for(j=0;j<N;j++)
        {
            if(a[i][j]<min)
                min=a[i][j];
        }
    }
    return min;
}
```

## 二、指针

### 1.指针变量

##### 1.1指针变量的定义和初始化

1.定义

```c
datatype *name;
//datatype表示指针变量所指数据的类型,*表示一个指针变量
```

例如:

```c
int *pa;
char *pb;
```

2.初始化

```c
#include<stdio.h>
int main()
{
    int a=0,b=1;
    char c='A';
    int *pa,*pb;
    char *pc;
    pa=&a;//指针的内容必须为地址值
    pb=&b;
    pc=&c;
    printf("a is %d,&a is %p,pa is %p,&pa is %p\n",a,&a,pa,&pa);
    printf("b is %d,&b is %p,pb is %p,&pb is %p\n",b,&b,pb,&pb);
    printf("c is %c,&c is %p,pc is %p,&pc is %p\n",c,&c,pc,&pc);
    return 0;
}
```

如果不知道指针要指向谁,习惯上在定义指针变量时将其初始化为NULL

指针变量只能指向同一基类型的变量

##### 1.2用指针变量作函数参数

从键盘输入两个整数,用指针变量作为函数的参数,编程互换这两个数并输出

```c
#include<stdio.h>
void swap(int *x,int *y)
{
    int temp;
    temp=*x;
    *x=*y;
    *y=temp;
}
int main()
{
    int a,b;
    printf("请输入a和b的值:");
    scanf("%d %d",&a,&b);
    printf("交换前a=%d,b=%d\n",a,b);
    swap(&a,&b);
    printf("交换后a=%d,b=%d\n",a,b);
    return 0;
}
```

### 2.函数指针

##### 2.1函数指针的定义

```c
int(*f)(int a);//函数指针
int *f(int a);//指针函数
```

##### 2.2函数指针的应用

```c
#include<stdio.h>
#include<string.h>
char * fun(char *p1,char *p2)
{
    int i=0;
    i=strcmp(p1,p2);
    if(0==i)
        return p1;
    else
        return p2;
}
int main()
{
    char *(*pf)(char *p1,char *p2);
    pf=&fun;
    (*pf)("AA","BB");
    return 0;
}
```

函数指针在实际应用当中主要用于函数的回调



