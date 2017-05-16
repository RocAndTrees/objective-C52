# Effective Object-C 52：37-46
### 六、块与大中枢派发

> 块（block） 、大中枢派发（Grand center Dispatch， GCD）
>
>  语法闭包（lexical closure）

#### 37.理解“块”这一概念

* 块石C、C++、Objective-C中的语法闭包
* 可以接受参数、返回值
* 根据范围：“栈块”、“堆块”、“全局块”。分配在栈上的块可以拷贝到堆中，这样的话就和标准的Objective-C对象一样，具备引用计数能力。


##### 基础

块的语法结构：

`return_type (^block_name)(parameters)`

一般应用：
内联块（inline block）直接内联在函数调用中使用。
`numerateObjectsUsingBlock:`


##### 块的内部结构
图1

##### “栈块”、“堆块”、“全局块”。
一开始定义的块其所占的内唇区域是分配在栈内。通过copy 就会分配到堆中。

全局块：不会捕捉任何状态，运行时也无须有状态来参与。所使用的整个内存区域，在编译器已经完全确定，全局块可以声明在全局内存里。


#### 38. 为常用的块类型创建typedef

* 使用typedef重新定义块类型，令块变量用起来更加简单。

因为每个块都具备“固有类型”（inherent type），因此可以赋给适当类型的变量。

```
^(BOOL flag, int value){
    if (flag) {
        return value * 5;
    }else{
        return value * 10;
    }
    
};
  
//变量类型以及赋值语句  
int(^variableName)(BOOL flag, int value) = ^(BOOL flag, int value){
    return 1;
};
    
variableName(YES, 10);

//块类型的语法结构
return_type (^block_name)(parameters)
```

使用C语言中“类型定义”（type definition）特性
例子：

```
typedef int(^EOCSomeBlock)(BooL flag, int value);

EOCSomeBlock block = ^(BOOL flag, int value){
        //Implementation
}

block(YES, 10);
```

#### 39.用handler 块降低代码分散程度

* 创建对象时，可以使用内联的handler 块将相关业务逻辑一并声明。
* 在有多个实例需要监控时：
  1. 委托模式：需要经常根据传入的对象来切换
  2. 块: 可以直接将相关块和对象放在一起。
* 设计API的时候如果用到handler块，可以增加一个参数，通过这个参数来决定把块安排到哪里队列上执行。<可能废除了>



#### 40.用块引用其所属对象时不要出现保留环

* 如果块所捕获的对象直接或间接保留了块本身，那么就得当心保留环问题
* 一定要找个适当的时机解除保留环。`<weak, weakSelf, strongSelf>`



#### 41. 多用派发队列，少用同步锁




#### 42.
#### 43.
#### 44.
#### 45.
#### 46.
