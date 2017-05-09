# Effective Object-C 52：15-22
### 三、接口与API设计

#### 15. 用前缀避免命名空间冲突
* 选择公司、应用程序、其一二之名作为类名的前缀，并在所有代码均使用这一前缀
* 为项目中使用第三方库加上前缀。（一般不用）

OC 没有内置的命名空间（namespace）机制，所以如果命名重名，就会发送命名冲突（naming calsh）项目报错。

重命名符号错误（duplicate symbol error）报错：

```
duplicate symbol _OBJC_METACLASS_$_EOCTheClass in:
	build/something.o
	build/something_else.o
duplicate symbol _OBJC_CLASS_$_EOCTheClass in:
	build/something.o
	build/something_else.o
```

解决方案：

1. 所有名称都加上适量前缀。
2. 使用3字母 != Apple Cocoa（两字母前缀 two_letter prefix）。

#### 16. 提供“全能初始化方法”

* 在类中提供一个全能初始化方法，并在文档中指明。其他初始化方法均调用次方法。
* 若全能初始化方法与超类不同， 则需要覆写超类中对应的方法
* 超类的初始化不适用子类，应该覆写超类的方法，并在其中抛出异常。

 全能初始化（指定初始化方法）（designated initializer）：对象提供必要信息以便其能完成工作的初始化方法。
这个类多个初始化方法，其他初始化方法调用全能初始化。


覆写父类的全能初始化方法并在其中抛出异常：

```
-(id) initWithWidth:(float)width andHeight:(float)height{
    @throw [NSException exceptionWithName:NSInternalInconsistencyException reason:@"Must use initWithDimension: instead." userInfo:nil];
}
```


#### 17. 实现description方法

* 实现description方法返回有意义的字符串，用以描述该实例。
* 调试时候打印：实现debugDescription方法。

在类里添加实现方法 description、 debugDescription

```
-(NSString *)description{
    return [NSString stringWithFormat:@"%@, %@",[self class], self];
}
-(NSString *)debugDescription{
    return [NSString stringWithFormat:@"%@, %@",[self class], self];
}

```


#### 18. 尽量使用不可变对象

* 尽量创建不可变的对象。
* 某些属性仅可用于对象内部修改，则在“calss-continuation 分类” 中将其由readonly属性扩张为readwrite属性。
* 不要把可变的collection作为属性公开，而应提供相关的方法，以此修改对象中可变的collection。

例子： 在类 head 里实现readonly  在“calss-continuation 分类”  readwrite。

```
@interface CustomViewController:UIViewController

@property(nonatomic, copy, readonly) NSString* identifier;

@end

@interface CustomViewController ()

@property(nonatomic, copy, readwrite) NSString* identifier;

@end

```


#### 19. 使用清晰而协调的命名方式

* 遵从标准的Object-C 命名规范。
* 言简意骇，从左至右读起来要像个日常用语（最好）
* 不要使用缩略后的类型
* 风格符合自己的代码或者集成的框架。


#### 20. 为私有方法添加前缀



#### 21. 理解Object-C 错误模型

#### 22. 理解NSCoping 协议

