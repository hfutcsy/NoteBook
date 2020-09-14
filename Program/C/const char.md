# const char *, char const *, char * const 对比
指针和字符之间的关系

![https://images2018.cnblogs.com/blog/1434802/201808/1434802-20180830113118934-1315777086.png](https://images2018.cnblogs.com/blog/1434802/201808/1434802-20180830113118934-1315777086.png)

## 1. const char *ptr
定义一个指向字符常量的指针，ptr是一个指向char*类型的常量，所以不能用ptr来修改所指向的内容，*ptr的值为const，不能修改。但是ptr的声明并不意味着它指向的值实际就是一个常量，而只是意味着对ptr而言，这个值是常量。实验如下：ptr指向str,而str不是const，可以直接通过变量来修改str的值，但是却不能通过ptr指针来修改。
```
#include <iostream>

using namespace std;

int main()
{
int i;
char str[] = "hello world";
char str[] = "good name";
const char *ptr = str;
for (int i = 0; i < 11; i++)
cout << ptr[i];
cout << endl;

// assignment of read-only location *ptr
ptr[0[ = 's';	// 通过ptr修改， 报错
str[0] = 'g'; 	// 通过str修改， 正常

// 可以通过重新复制给该指针来修改其所指向的值
// ptr = ss;	// 重新赋值ptr指针
for (int i = 0; i < 11; i++)
cout << ptr[i];

cout << endl;
return 0;
}
```
## 2. char const *ptr
与const char* ptr等价
## 3. char * const ptr
定义一个指向字符的指针常数，即const指针，不能修改ptr指针，并且声明必须初始化，但可以修改其指向的内容。实验:
```
#include <iostream>

using namespace std;

int main()
{
int i;
char str[] = "hello world"
char ss[] = "good game!";
char * const ptr = str;

for (int i = 0; i < 11; i++)
cout << ptr[i];
cout << endl;
ptr[0] = 's';	// 通过ptr修改， 正常

// assignment of read-only variable
ptr = ss;	// 重新赋值ptr， 报错
for (int i = 0; i < 11; i++)
cout << ptr[i];
cout << endl;

return 0;
}
```

## Reference
+ <https://blog.csdn.net/gripex/article/details/103303291>
+ <https://www.cnblogs.com/wzqstudy/p/9559255.html>