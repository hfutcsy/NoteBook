# wchar_t and char
## 定义
**char**是8位字符类型，最多只能包含256种字符，许多外文字符集所含的字符数目超过256个，char型无法表示。

**wchar_t**数据类型一般为16位或32位，但不同的C或C++库有不同的规定，如GNU Libc规定wchar_t为32位，总之，wchar_t所能表示的字符数远超char型。


通常用 L"" 表示wchar_t。

    ```
    "A"    = 41
    "ABC"  = 41 42 43
    L"A"   = 00 41
    L"ABC" = 00 41 00 42 00 43
    ```

## 相互转换
### 方法一：WideCharToMultiByte（）和 MultiByteToWideChar()
#### wchar_t   转为  char
使用函数 WideCharToMultiByte()
```
wchar_t* pwszUnicode = L"Holle";  //wcslen(pwsUnicode)=5
int iSize;
char* pszMultiByte;//返回接受字符串所需缓冲区的大小，已经包含字符结尾符'\0'
iSize = WideCharToMultiByte(CP_ACP, 0, pwszUnicode, -1, NULL, 0, NULL, NULL); //iSize =wcslen(pwsUnicode)+1=6
pszMultiByte = (char*)malloc(iSize*sizeof(char)); //不需要 pszMultiByte = (char*)malloc(iSize*sizeof(char)+1);
WideCharToMultiByte(CP_ACP, 0, pwszUnicode, -1, pszMultiByte, iSize, NULL, NULL);
```
#### char  转为  wchar_t
使用函数 MultiByteToWideChar()
```
char* pszMultiByte = "Holle";  //strlen(pwsUnicode)=5
int iSize; wchar_t* pwszUnicode ; 
//返回接受字符串所需缓冲区的大小，已经包含字符结尾符'\0'
iSize = MultiByteToWideChar(CP_ACP, 0, pszMultiByte , -1, NULL, 0); //iSize =wcslen(pwsUnicode)+1=6
pwszUnicode = (wchar_t *)malloc(iSize*sizeof(wchar_t)); //不需要 pwszUnicode = (wchar_t *)malloc((iSize+1)*sizeof(wchar_t))
MultiByteToWideChar(CP_ACP, 0, pszMultiByte , -1, pwszUnicode , iSize);
```
### 方法二：用stdlib.h中的mbstowcs_s() 和 wcstombs_s()
#### wchar_t   转为  char
stdlib.h中的wcstombs_s函数
```
#include <stdlib.h>wchar_t *WStr = L"string to convert";

size_t len = wcslen(WStr) + 1;

size_t converted = 0;

char *CStr;

CStr=(char*)malloc(len*sizeof(char));

wcstombs_s(&converted, CStr, len, WStr, _TRUNCATE);
```
#### char  转为  wchar_t
stdlib.h中的mbstowcs_s函数
```
#include <stdlib.h>
char *CStr = "string to convert";

size_t len = strlen(CStr) + 1;

size_t converted = 0;

wchar_t *WStr;

WStr=(wchar_t*)malloc(len*sizeof(wchar_t));

mbstowcs_s(&converted, WStr, len, CStr, _TRUNCATE);
```
### 方法三： 用流的方式单向转换（（const） char* --> const wchar_t*)
#### 只能从（const） char* --> const wchar_t*，并且转换结果是const类型。
```
#include<sstream>

char *cstr="string to convert";

wstringstream wss;

wss<<cstr;

const wchar_t* wchar=wss.str().c_str()
```

## Reference
+ [百度百科](https://baike.baidu.com/item/wchar_t)
+ [wchar_t 和 char 之间转换](https://www.cnblogs.com/vranger/p/3792791.html)
