## 类变量

苹果推荐在现代 Objective-C 中使用 ```@property``` 来实现成员变量：

``` objc
@interface AClass : NSObject

@property (nonatomic, copy) NSString *name;

@end
```

```@property```  可以看做是一种语法糖，使用 ```@property``` 会自动生成 getter 和 setter，同时进行自动内存管理。

```@property``` 的属性修饰可以有以下几种：

* readwrite 是可读可写特性；会生成 getter 方法和 setter 方法
* readonly 是只读特性；只会生成 getter 方法，不会生成 setter 方法，不希望属性在类外改变时使用
* assign 是赋值特性；setter 方法将传入参数赋值给实例变量；仅设置变量时
* retain 是持有特性；setter 方法将传入参数先保留，再赋值，传入参数的 retain count 会+1
* copy 是拷贝特性；setter 方法将传入对象复制一份；需要完全一份新的变量时
* atomic 和 nonatomic，决定编译器生成的 setter getter 是否是原子操作。atomic 表示使用原子操作，可以在一定程度上保证线程安全。一般推荐使用 nonatomic， 因为 nonatomic 编译出的代码更快

默认的 ```@property``` 是 readwrite、assign、atomic。

同时，我们还可以使用自定义的 accessor 的名字：

``` objc
@property (getter=isFinished) BOOL finished;
```

这种情况下，编译器生成的 getter 方法名为 ```isFinish```，而不是 ```finished```。

---

## ```@synthesize``` 和 ```@dynamic``` 分别有什么作用？

* ```@property``` 有两个对应的词，分别是 ```@synthesize``` 和 ```@dynamic```。如果 ```@synthesize``` 和 ```@dynamic``` 都没写，默认的就是 ```@synthesize var = _var```
* ```@synthesize``` 的语义是如果你没有手动实现 setter 和 getter，那么编译器会自动为你实现这两个方法
* ```@dynamic``` 告诉编译器：属性的 setter 和 getter 方法由用户自己实现，不需要自动生成。（当然，对于 readonly 的属性只需提供 getter 即可）。如果一个属性被声明为 ```@dynamic var```，然后你没有提供 setter 和 getter，编译的时候没有问题，但是当程序运行到 ```instance.var = someVar```，由于缺少 setter 方法会导致程序崩溃；或者当运行到 ```someVar = var``` 时，由于缺少 getter 方法同样会导致崩溃。