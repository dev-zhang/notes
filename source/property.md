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

