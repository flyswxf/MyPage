---
title: 引用和复制
---

```cpp
class Example{
    string str;
public:
    Example(){}
    Example(string s): str(s){}
    string& getStr(){
        return str;
    }
};

int main(){
    Example e("Hello");
    string s = e.getStr();
    s+='a';
    cout<<e.getStr()<<endl;
    cout<<s<<endl;
    return 0;
}
```
这段代码中,`getStr()`返回了`str`的引用,将引用赋值给s后,我希望 __通过改变s改变e.str__

然而结果为
```
Hello
Helloa
```

原因是在将`str`的引用赋值给`s`时,`s`变成`str`的一个副本,而不是直接指向同一个字符串对象的引用。这是因为 `s` 被声明为一个新的 `string` 对象，所以当对 `s` 进行修改时，这个修改不会反映到原始的 `str` 成员变量上。

修改方法为 __将s声明为引用类型__
```cpp
string& s = e.getStr();
```

这样，s 就成为了 str 的一个别名，对 s 的任何修改都会直接反映到 e 中的 str 上。