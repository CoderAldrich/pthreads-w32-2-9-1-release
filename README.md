# pthreads-w32-2-9-1-release
pthreads-w32-2-9-1-release  [ftp://sources.redhat.com/pub/pthreads-win32/](ftp://sources.redhat.com/pub/pthreads-win32/)

直接使用or编译源码
## 直接使用
Pre-built.2这个文件夹下有三个文件夹
dll 动态链接库
include头文件
lib 静态链接库
### 配置头文件
把include文件夹下的头文件拷贝到vs2017安装目录下

D:\Program Files (x86)\Microsoft Visual Studio\2017\Professional\VC\Tools\MSVC\14.11.25503\include\
### 配置静态链接库
把lib文件夹下的静态库文件拷贝到vs2017安装目录下

D:\Program Files (x86)\Microsoft Visual Studio\2017\Professional\VC\Tools\MSVC\14.11.25503\lib
### 配置动态链接库
Pre-built.2\dll\x86下的文件拷贝到C:\Windows\SysWOW64目录下 
Pre-built.2\dll\x64下的文件拷贝到C:\Windows\System32目录下

测试
```
#include <pthread.h>
#pragma comment(lib,"pthreadVC2.lib")
int main()
{
    return 0;
}
```
编译错误C2011 “timespec”:“struct”类型重定义
可修改pthread.h文件，在
```
#if !defined( PTHREAD_H )
#define PTHREAD_H
```
下面加上一行宏定义
```
#ifdef WIN32
#define  HAVE_STRUCT_TIMESPEC
#endif
```
可以解决“timespec”:“struct”类型重定义错误

至此，已经可以在VS2017中使用。如果不想改动到VS2017的目录和系统目录，可以通过配置工程项目属性，设置附加包含目录/链接器附加依赖库等选项，从而达到使用pthread库的目的。
