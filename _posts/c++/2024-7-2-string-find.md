---
layout: "post"
title: string::find
category: C++ 
---

# 常量
## **`string::npos`**:
`string::npos`是`string`类中定义的一个常量，表示无效的位置或最大可能的字符串长度。通常用于表示查找操作失败。

# 函数
## **`find`**

### 基本用法

```cpp
size_t pos = str.find(sub, pos);
```

### 参数和返回值

- **参数**：
  - `sub`：要查找的子串或字符。
  - `pos`：开始查找的位置，默认为0，即从字符串的开始位置查找。
- **返回值**：如果找到子串或字符，返回其在字符串中的起始位置索引；如果未找到，返回`string::npos`。
### 实例
```cpp
while ((pos = s1.find(s2, pos)) != string::npos)
    {
        pos+=s2.size();
    }
```



