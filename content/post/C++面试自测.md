---
title: "C++ 自测"
date: 2021-03-10T01:37:56+08:00
lastmod: 2021-03-10T01:37:56+08:00
draft: false
tags: ["面试", "C/C++"]
categories: ["notes"]
author: "magictomagic"
contentCopyright: '<a rel="license noopener" href="https://en.wikipedia.org/wiki/Wikipedia:Text_of_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License" target="_blank">Creative Commons Attribution-ShareAlike License</a>'
---


>要了解底层原理，
>不仅仅是概念，还要实现

## memcpy memmove
>With memcpy, the destination cannot overlap the source at all. With memmove it can. This means that memmove might be very slightly slower than memcpy, as it cannot make the same assumptions.
<details>
<summary>Click to expand!</summary>

```C++
void * __cdecl memcpy ( void * dst,const void * src,size_t count){
  void * ret = dst;
  while (count--){ // 注意， memcpy函数没有处理dst和src区域是否重叠的问题
    *(char *)dst = *(char *)src;
    dst = (char *)dst + 1;
    src = (char *)src + 1;
  }
  return(ret);
}

void * __cdecl memmove (void * dst,const void * src,size_t count){
  void * ret = dst;
  if (dst <= src || (char *)dst >= ((char *)src + count)){ // 若dst和src区域没有重叠，则从起始处开始逐一拷贝
    while (count--){
      *(char *)dst = *(char *)src;
      dst = (char *)dst + 1;
      src = (char *)src + 1;
    }
  }else{ // 若dst和src 区域交叉，则从尾部开始向起始位置拷贝，这样可以避免数据冲突
    dst = (char *)dst + count - 1;
    src = (char *)src + count - 1;
    while (count--){
      *(char *)dst = *(char *)src;
      dst = (char *)dst - 1;
      src = (char *)src - 1;
    }
}
return(ret);
```
</details>

---

## 构造函数的显示和隐式调用

<details>
<summary>Click to expand!</summary>

```c++
class Test1{
  public:
    Test1(int n){
        num=n;
    }//普通构造函数
  private:
    int num;
};
class Test2{
  public:
    explicit Test2(int n){
        num=n;
    }//explicit(显式)构造函数
  private:
    int num;
};
int main(){
  Test1 t1=12;//隐式调用其构造函数,成功
  Test2 t2=12;//编译错误,不能隐式调用其构造函数
  Test2 t2(12);//显式调用成功
  return 0;
}
```

Test1的构造函数带一个int型的参数，代码23行会隐式转换成调用Test1的这个构造函数。而Test2的构造函数被声明为explicit（显式），这表示不能通过隐式转换来调用这个构造函数，因此代码24行会出现编译错误。 普通构造函数能够被隐式调用 。而explicit构造函数只能被显式调用。

</details>

<!-- <textarea onkeyup="_mdAdjustTextareaHeight(this)" rows="10" style="overflow: scroll; border-top-left-radius: 0; border-top-right-radius: 0;"></textarea> 维护一个全局输入框，类似leetcode的高亮与编码模式-->

---


## 大端小端检测方法

<details>
<summary>Click to expand!</summary>

大端模式，是指数据的高字节位保存在内存的低地址中，而数据的低字节位保存在内存的高地址中。

小端模式，是指数据的高字节位 保存在 内存的高地址中，而数据的低字节位保存在 内存的低地址中。

```c++
int i = 1;
char *p = (char *)&i;
if(*p == 1) printf("Little Endian");
else printf("Big Endian");
```

</details>

---

## 拷贝(复制)构造函数

<details>
<summary>Click to expand!</summary>

</details>

---

## 智能指针

### 引用计数
引用计数这种计数是为了防止内存泄露而产生的。 基本想法是对于动态分配的对象，进行引用计数，每当增加一次对同一个对象的引用，那么引用对象的引用计数就会增加一次， 每删除一次引用，引用计数就会减一，当一个对象的引用计数减为零时，就自动删除指向的堆内存。

### RAII
对于一个对象而言，我们在构造函数的时候申请空间，而在析构函数（在离开作用域时调用）的时候释放空间， 也就是我们常说的 RAII 资源获取即初始化技术(resource acquisition is the initialization technology.)。

在传统 C++ 里我们只好使用 new 和 delete 去 『记得』对资源进行释放。而 C++11 引入了智能指针的概念，使用了引用计数的想法，让程序员不再需要关心手动释放内存。 这些智能指针就包括 std::shared_ptr/std::unique_ptr/std::weak_ptr，使用它们需要包含头文件 `<memory>`。

智能指针就是一个类，当超出了类的作用域是，类会自动调用析构函数，析构函数会自动释放资源。



## 多态 重载 重写

---

## 堆和栈的区别

---

## 编写 Socket 套接字

---

## extern "C"

---

## 哪些成员函数不能被继承










# 学院派自测 #

## 进程和线程的区别

## 多进程与多线程的区别

## 线程间通信方式及优缺点

## 进程间通信方式及优缺点




## 设计模式高频

# Linux 后端开发自测 #

## unix/linux下的进程间通信和各自的特点

## epoll

## fork



std::move

unique_ptr

std::move 移动构造函数，左值变右值