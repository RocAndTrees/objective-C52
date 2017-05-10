# Effective Object-C 52：29-36
### 四、内存管理

>自动引用计数（Automatic Reference Counting， ARC）

#### 29.理解引用计数

* 引用计数机制通过递增递减的计数器来管理内存。创建成功后是 1， 降为0时对象销毁。
* 对象生命周期中，其余对象通过引用来保留或释放次对象。保留、释放操作对象的计数器递增、递减。

##### 引用计数工作原理
引用计数架构下，对象有个计数器根据计数的字来确认是否释放对象或者保留，Object-C 中叫“保留计数”（retain count）／“引用计数”（reference count）。

* Retain：递增
* release： 递减
* autorelease： 自动释放池（autorelease pool）

图1

例子（MRC情况下手动添加释放 retain count）：

```
NSMutableArray *array = [[NSMutableArray alloc] init];
    
    NSNumber *number = [[NSNumber alloc] initWithInt:1000];
    
    [array addObject:number];
    [number release];
    
    //do something with 'array'
    
    [array release];

```

图2

##### 保留环（retain cycle）
环状互相引用多个对象，导致内存泄漏。
图3

解决方案：1. “弱引用”（weak reference）  2.从外界命令循环中的某个对象不再保留另一个对象。



#### 30.以ARC简化引用计数

* 手动“保留”、“释放”->自动化。
* ARC只负责Objective-C对象的内存。





#### 31.
#### 32.
#### 33.
#### 34.
#### 35.
#### 36.
