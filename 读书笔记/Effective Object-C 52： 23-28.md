# Effective Object-C 52：23-28
### 四、协议与分类

Object-C 语言特性： “协议” （protocol）、“分类”（Category）

#### 23.通过委托与数据源协议进行对象间通信

* 委托模式为对象提供一套接口，对象间事件通知方法之一。
* 将委托对象支持接口定义的协议，在协议中把需要处理的事件定义成方法。
* 若有必要，可以实现有位段的结构体，将委托对象是否能响应相关协议这个信息缓存。

委托模式：定义一套接口，对象若想接受另一个对象的委托，则需要遵从此接口。 委托对象（delegate）
数据源模式：数据源（Data Source）流向类（Class） 
图2
![网络请求整体流程图](https://raw.githubusercontent.com/RocAndTrees/objective-C52/master/resource/image/objec-c52/13-2操作后的映射表.png)

例子网络请求整体流程图：

![网络请求整体流程图](https://raw.githubusercontent.com/RocAndTrees/objective-C52/master/resource/image/objec-c52/13-2操作后的映射表.png)


本对象和委托对象之间的所有权关系：

![本对象和委托对象之间的所有权关系图](https://raw.githubusercontent.com/RocAndTrees/objective-C52/master/resource/image/objec-c52/13-2操作后的映射表.png)


协议定义：

```
@protocol EOCNetWorkFetcherDelegate 

@optional
- (void)netWorkFetcher:(id)fetcher
        didReceiveData:(NSData*)data;
- (void)netWorkFetcher:(id)fetcher
        didFailWithError:(NSData*)data;
- (void)netWorkFetcher:(id)fetcher
        didUpdataProgressTo:(NSData*)data;

@end

```
此类的接口定义：

```
@interface EOCNetWorkFetcher : NSObject

@property (nonatomic, weak) id<EOCNetWorkFetcherDelegate> deleage;

@end

```
委托对象调用可选方法(+判断委托对象是否响应相关选择子)：

```
if ([_deleage respondsToSelector:@selector(netWorkFetcher:didReceiveData:)]) {
        [_deleage netWorkFetcher:self didReceiveData:data];
    }

```

如果需要经常使用响应特定的选择子，频繁的执行检察工作没有必要，可以通过结构体、位段（bitfield）数据类型 来缓冲判断：

```
struct data {
    unsigned int didReceiveData : 1;
    unsigned int didFailWithError : 1;
    unsigned int didUpdataProgressTo : 1;
 } _deleageFlags;
// set flag
_delegateFlags.didReceiveData = 1;   
//_deleageFlags.didReceiveData = [_deleage respondsToSelector:@selector(netWorkFetcher:didReceiveData:)];
// Check flag
if (_delegateFlags.didReceiveData){
	//Yes , flag set
}

```

#### 24.将类的实现代码分散到便于管理的数个分类之中

* 使用分类机制把类的实现代码划分成易于管理的小块
* 将“私有”的方法归入名为 Private的分类中，以隐藏实现细节。

例子： 

```
@interface EOCPerson （Friendship)
-(void)addFriend:(EOCPerson*)person;
-(void)removeFriend:(EOCPerson*)person;
-(void)isFriendWith:(EOCPerson*)person;
@end

@interface EOCPerson （Work)
-(void)performDaysWork;
-(void)takeVacationFromWork;
@end

@interface EOCPerson （Play)
-(void)goToTheCinama;
-(void)goToSportsGame;
@end



@implementation EOCPerson(Friendship) 
-(void)addFriend:(EOCPerson*)person{
	/* ... */
}
-(void)removeFriend:(EOCPerson*)person{
	/* ... */
}
-(void)isFriendWith:(EOCPerson*)person{
	/* ... */
}

@end
```

#### 25.总是为第三方类的分类名称加上前缀

 
 

#### 26.
#### 27.
#### 28.