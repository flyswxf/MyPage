---
title: How to compile multiple tasks in VScode
---

假设我们编写了一个简单的类实现`C++`代码

## `circle.h`
```cpp
class Circle
{
private:
    double r, x, y;
    const double PI = 3.14159;

public:
    Circle(double r, double x, double y);
    void getInfo();
    double getArea();
    double getCircumference();
};
```
## `Circle.cpp`
```cpp
#include "Circle.h"
#include <iostream>
using namespace std;

Circle::Circle(double r, double x, double y) : r(r), x(x), y(y) {}

void Circle::getInfo()
{
    cout << "radius: " << r << " xPoint: " << x << " yPoint: " << y << endl;
}

double Circle::getArea()
{
    return PI * r * r;
}

double Circle::getCircumference()
{
    return 2 * PI * r;
}
```

## `work.cpp`
```cpp
#include <iostream>
#include <fstream>
#include "Circle.h"
using namespace std;

int main()
{
    ifstream inFile("infomation.txt");
    double r, x, y;
    if (!inFile)
    {
        cout << "Error" << endl;
        return 1;
    }
    while (inFile >> r >> x >> y)
    {
        Circle c(r, x, y);
        c.getInfo();
        cout << "area is " << c.getArea() << endl;
        cout << "circumference is " << c.getCircumference() << endl;
        cout << endl
             << endl;
    }
    inFile.close();
}
```
代码本身没有错误,符合规范,也不会在问题区发现任何报错信息

__但是,在work.cpp中尝试运行代码时,却会出现错误信息:__
```
work.obj : error LNK2019: 无法解析的外部符号 "public: double __thiscall Circle::getCircumference(void)" (?getCircumference@Circle@@QAENXZ)，函数 _main 中引用了该符号
```
总共四个类成员函数全部出现链接错误
# 问题出在哪?

## 1. 程序运行需要什么?
类分装成.h(头文件)和.cpp(实现文件)
 - `.h`头文件只包含了声明而没有实际的执行代码，所以它们不需要直接被编译
 - `.cpp` 文件是 C++ 程序的源代码文件，包含了程序的实际执行代码,需要编译才能运行

即使是没有入口(main)的Circle.cpp,也需要编译,才能够被正确链接

链接是:
```
将程序中使用的不同 .cpp 文件和库文件合并成一个可执行文件
```


## 2. `vscode`干了什么

当点击按钮运行`cpp`程序时,`vscode`实际上打开了一个命令行文件,输入了编译并执行的指令
```
cmd /c chcp 65001>nul && cl.exe /Zi /EHsc /nologo /FeD:\HuaweiMoveData\Users\fengl\Desktop\work.exe D:\HuaweiMoveData\Users\fengl\Desktop\work.cpp
```
显然里面没有包含`Circle.cpp`的编译信息,__`vscode`不会自动编译头文件的依赖!!__

那么如何编译呢?

### 最朴素的方法是手动编译
1. 打开`cmd`
2. 输入命令->`cl.exe /EHsc work.cpp Circle.cpp`,使用`cl`(Microsoft的编译器)对两个`cpp`文件进行编译

```
用于 x86 的 Microsoft (R) C/C++ 优化编译器 19.38.33135 版
版权所有(C) Microsoft Corporation。保留所有权利。

work2.cpp
Circle.cpp
正在生成代码...
Microsoft (R) Incremental Linker Version 14.38.33135.0
Copyright (C) Microsoft Corporation.  All rights reserved.

/out:work.exe
work.obj
Circle.obj
```
3. 编译成功,得到`work.exe`,运行即可

### 用vscode自身实现编译
当我们点击运行按钮运行`C++`文件后(不管是否运行成功),`vscode`会自动在工作目录创建`.vscode`目录,里面包含一个`task.json`文件
```json
{
    "tasks": [
        {
            "type": "cppbuild",
            "label": "C/C++: cl.exe 生成活动文件",
            "command": "cl.exe",
            "args": [
                "/Zi",
                "/EHsc",
                "/nologo",
                "/Fe${fileDirname}\\${fileBasenameNoExtension}.exe",
                "${file}"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$msCompile"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "调试器生成的任务。"
        }
    ],
    "version": "2.0.0"
}
```
其中的`file`就是指当前运行的`.cpp`文件
将它改成`"${workspaceFolder}/*.cpp"`
 - `workspaceFolder`代表当前工作区的根目录
 - `/*.cpp`用于匹配所有在workspaceFolder下的.cpp文件

这样在运行`work.cpp`时,`vscode`会自动编译当前工作区根目录下的所有`.cpp`文件,自然就会包括`work.cpp`和`Circle.cpp`了

