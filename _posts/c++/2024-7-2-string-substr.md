---
layout: post
title: Substr
category: C++
---

# 函数原型
```cpp
string substr(size_t pos = 0, size_t len = npos) const;
```

## 参数
- `pos` 参数指定了子字符串开始的位置（位置从 0 开始计数）。
- `len` 参数指定了子字符串的长度。__如果 `len` 超过了原字符串的剩余长度，则函数会返回从 `pos` 开始到原字符串末尾的所有字符。__
## 返回值
- 该函数返回一个新的字符串对象，包含从 `pos` 开始、长度为 `len` 的子字符串。

## 例子
```cpp
#include <iostream>
#include <string>

int main() {
    std::string str = "Hello, World!";
    // 使用substr获取"World"
    std::string subStr = str.substr(7, 5);

    std::cout << "Original string: " << str << std::endl;
    std::cout << "Substring: " << subStr << std::endl;

    return 0;
}
```
## 运行结果

```
Original string: Hello, World!
Substring: World
```