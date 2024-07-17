---
title: 文件输入输出
date: 2024-07-03
---

## 1.头文件
`fstream>`,包含了`ofstream`和`ifstream`


### 写入文件的例子
```cpp
    ofstream outFile("example.txt");
    //也可以使用outFile.open("example.txt");
    if(outFile.is_open()){
        outFile << "Hello, World!\n";
        ... 
        outFile.close();
    }
    else{
        cerr << "Failed to open example.txt for reading.\n";
        return 1;
    }
```

### 读取文件的例子
```cpp
    ifstream inFile("example.txt");
    string line;
    if (inFile.is_open()) {
        while (getline(inFile, line)) { // 逐行读取
            cout << line << '\n';
        }
        inFile.close(); // 关闭文件
    }
    else{
        cerr << "Failed to open example.txt for reading.\n";
        return 1;
    }
```

## 2. 文件路径

- **绝对路径**：从根目录或驱动器的开始位置指定的完整路径。
如:

```cpp
string filePath = "C:\\path\\to\\your\\file.txt";
ifstream inFile(filePath);
```
__需要加双 `\\` ,因为在 C++ 字符串中，反斜杠 `\` 被用作转义字符的前缀__

但是也可以选择
```cpp
string filePath = R"(C:\path\to\your\file.txt)";
```
R前缀代表Raw string,不会对转义字符`\`做处理
- **相对路径**：相对于当前工作目录的路径。
 
