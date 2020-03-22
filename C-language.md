## C语言基础

### 指针

由引用类型T派生的指针类型有时称为“(指向) T的指针”。

- **将数组作为形参传递**

  数组名可以理解为指向数组初始元素的指针，也可以理解为数组名是数组首元素的地址。

  如果试图将数组作为函数参数进行传递，其实传递的是指向数组初始元素的指针。

```c
int a[10];
int *p;
p = &a[0];	//与下一行等价
p = a; 		//数组名可以理解为指向数组初始元素的指针，也可以理解为数组名是数组首元素的地址
p[i] = a[i] = *(p + i);
```

以下两种写法等价：

```c
int func(char *a[], int size);	//数组a[]中元素的类型是char *，a 是数组名，表示指向数组首元素的指针，其类型是char **
int func(char **a,  int size);	//char **a 是指向 char *a[0]的指针, char **a = &a[0];
//以上两种写法等效
```

### 可变参数

- 函数的参数是入栈顺序是从右至左，```int func(int a, int b, int c, int d)``` 在入栈的顺序中，d 最先入栈，a 最后入栈。
- *<stdarg.h>* 该头文件属于GCC。在GCC中已经用 *<stdarg.h>* 取代 *<varargs.h>* 。
- *<stdarg.h>* 中的 *macro*：
1. ```va_list``` ： 可变参数类型，```typedef char * va_list``` 

   ```
   va_list argp;	//argp可以理解为指向可变参数的指针
   ```

2. ```void va_start(va_list argp, pre_param)``` ： ```va_start``` 表示获取第一个可变参数，```pre_param``` 表示固定参数

3. ```void va_arg(va_list arpg, type)``` : type 表示该可变参数的类型

4. ```void va_end(va_list argp)``` : 与 ```va_start```成对出现

- 可变参数举例

  ``` c
  int sum(int num, ...)	//声明中至少需要一个固定参数
  {
      int sum = 0;
      int para;
      va_list argp;		//定义可变参数指针
      va_start( argp, num );	//获取num后的第一个可变参数，argp指向num后的第一个可变参数
      while(num)
      {
          para = va_arg( argp, int); 	//可变参数的类型
          sum += para;
          num--;
      }
      va_end(argp);	//与va_start成对出现
      return sum;
  }
  ```

  