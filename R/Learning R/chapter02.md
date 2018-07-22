# 《Learning R》笔记之 Chapter 2 运算符号

chapter2探讨的是R中的运算符号、缺失值和逻辑运算符。  
首先，R是专门为向量运算做了优化的一门程序语言，两个向量之间可以直接进行运算，前提是二者长度相当，或一个是另一个的约数，此时短的一个向量会被循环以便匹配长的一个。如果二者长度互质，循环不会完整甚至报错，因此应当**尽量避免** 。
```r
    > 1:6 + 1:2
    [1] 2 4 4 6 6 8
    > 1:6 + 1:5
    [1]  2  4  6  8 10  7
    Warning message:
    In 1:6 + 1:5 :
    longer object length is not a multiple of shorter object length
```

同样，R中内置的常用数学函数也能够接受一个向量参数。
```r
    > cos(4:9)
    [1] -0.6536436  0.2836622  0.9601703  0.7539023 -0.1455000 -0.9111303
```
在比较两个数值大小时，常用运算符和其他语言类似，包括**== > < != >= <=** 。但需要注意的是，在比较浮点数大小时可能存在误差，因此如果真的要比较大小，考虑使用**all.equal()**.

```r
    > sqrt(3)^2 == 3
    [1] FALSE
    > all.equal(sqrt(3)^2 , 3)
    [1] TRUE
    > all.equal(sqrt(3)^2 , 2.9)
    [1] "Mean relative difference: 0.03333333" #如果要输出逻辑值，应用isTRUE() 作为wrapper
```

R中为变量赋值可以使用 **=** ， **<-** ，或者assign（‘variable_name’ , value）
R有3个特殊值：**Inf（infinite）** 、 **NaN（not a number）** 和 **NA（not avilable）**。要判断某个值是不是Inf、NaN或NA，不能使用==，而必须使用专门的函数：
```r
     x <- c(1,Inf,-Inf,NaN,NA)
    > is.na(x) ; is.infinite(x);is.nan(x) ; is.na(x)
    [1] FALSE FALSE FALSE  TRUE  TRUE
    [1] FALSE  TRUE  TRUE FALSE FALSE
    [1] FALSE FALSE FALSE  TRUE FALSE
    [1] FALSE FALSE FALSE  TRUE  TRUE
 ```
R中的逻辑运算符号还是 **！ &  |** 3种。注意，除了各个语言中保留的TRUE和FALSE（0以外所有实数都在逻辑运算中转换为TRUE，0转换为FALSE），NA也可以加入逻辑运算，此时结果需要 **额外小心**。
对于一个逻辑值构成的向量，**any()** 和 **all()** 可以接受这个向量，输出逻辑值，判断其中是否至少有一个或全为TRUE：
```r
    > x <- rnorm(10)
    > y <- x>= 0
    > any(y)
    [1] TRUE
```
