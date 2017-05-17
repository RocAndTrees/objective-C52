# Effective Object-C 52：47-52
### 七、系统框架

#### 47.熟悉系统框架
- 许多系统框架可以直接使用比如Fundation、coreFoundation
- 很多常见任务都用框架来实现。比如音频、视频处理，网络通讯，数据管理等。
- C写的框架和Object—C一样重要。


#### 48.多用块枚举、少用for循环

- collection 四种方法： 基本for循环、 NSEnumerator、快速遍历 for in、块枚举法 block。
- 块枚举法 本身就能通过GCD 来并发执行遍历操作，无须另写代码，其他遍历方式则无法轻易实现这一点。

#### 49.对自定义其内存管理语义的collection使用无缝侨接

- 通过无缝桥接技术，可以把Foundation框架中的Objective - C 对象与CoreFoundation框架中的C语言数据结构来回转换


例子：

```
NSArray *anArray = @[@1, @2, @3, @4, @5];
CFArrayRef aCFArray = (__bridge CFArrayRef)anNSArray;
NSLog(@"Size of array = %li", CGArrayGetCount(aCFArray));
//output : size of array = 5;

```



#### 50.构建缓存时选用NSCache 而非NSDiction
当遇到需要缓存网络下载下来的图片时候，应该是使用NSCache 来做。

* NSCache 可以提供优雅的自动删除功能，而且“线程安全的” 此外跟字典不同，并不会拷贝健。
* 可以给NSCache 对象设置上限，用来限制缓存中的对象总个数以及总成本。





#### 51.精简initialize 与 load的实现代码




#### 52.别忘了NSTimer会保留其目标对象

* NSTimer 对象会保留其目标，直到计时器本身失效为止，调用invalidate 方法可以让计时器失效，另外一次性的计时器在触发任务后也会失效。



