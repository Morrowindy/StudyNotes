# 《Learning R》笔记 Chapter 3 数据类型

从本章开始涉及到了数据类型。
R是一种面向对象的语言，储存的数据有不同的class，可以用**class()**查看。
常见的数值class包括numeric、integer，logical,character,factor等。这里需要额外提一句的是factor，它其实是带有string标签的interger，因此自带的attribute就包括levels（）和class（）：
```r
    > class(1.1);class(1);class(1L);class(1:4)
    [1] "numeric"
    [1] "numeric"
    [1] "integer"
    [1] "integer"

    > x <- sample(c('red','green'),10,replace = TRUE);class(x)
    [1] "character"
    > y <- factor(x,levels = c('red','green'));class(y);y;levels(y);nlevels(y)
    [1] "factor"
    [1] red   red   red   red   green red   red   green green green
    Levels: red green
    [1] "red"   "green"
    [1] 2
    > unclass(y)
     [1] 1 1 1 1 2 1 1 2 2 2
    attr(,"levels")
    [1] "red"   "green"
```
R中另有一大类array类型的数据类型，包括matrix，list等。  
要判断一个变量是不是某个class，输出一个逻辑值，那么应该使用**is.some_class()**，如is.atomic()，is.vector()等。同理，要转变class，应当使用**as.some_class()**。
```r
    > x <- 1.4353
    > class(x);as.integer(x);as.logical(x)
    [1] "numeric"
    [1] 1
    [1] TRUE #所有非零的**实数**转换成逻辑值后都为TRUE
    > as.integer(y) #factor转实数
     [1] 1 1 1 1 2 1 1 2 2 2
    > as.character(y)#factor转字符串
     [1] "red"   "red"   "red"   "red"   "green" "red"   "red"   "green" "green" "green"
```

在控制台打出的命令往往都默认带有一个print()，这样才能被我们看到。查看某个数据的结构，常用函数有**summary() , str() , View() , head()**.
列出当前workspace中的所有变量名，应使用**ls()**。  
这个函数还可以以** ls(pattern="某正则表达式") **的方式特定地列出某些变量名。  
rm(list=ls())删除当前所有变量。
