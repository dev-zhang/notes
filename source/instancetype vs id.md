## ```instancetype``` 和 ```id``` 的区别

1. ```instancetype``` 在类型表示上，和 ```id``` 一样，可以表示任何对象类型
2. ```instancetype``` 只能用在返回值类型上，不能像 ```id``` 一样用在参数类型上
3. ```instancetype``` 比 ```id``` 多一个好处：编译器会检测 ```instancetype``` 的真实类型

> 作为返回值类型时，凡是使用 ```id``` 的地方，都建议换成 ```instancetype```

