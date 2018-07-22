# 《Learning R》笔记 Chapter 5 上 list

从某个角度来说，R中的list对应的是Python中的dictionary。但list是能够利用序号index的，而dict不能,另外python中的dict使用哈希表实现的，原生的R没有哈希表。  
list就是一个典型的recursive型数据结构。is.atomic(某list)返回FALSE，而is.recursive(某list)返回TRUE。

##创建
创建list的基本语法是list （name = value）
```r
    > x <- list(
    +     2:5 , 
    +     month = month.abb ,  # month.abb 和month.name是两个内置变量名
    +     df = matrix(1:6 , nrow = 3))
    > x
    [[1]]
    [1] 2 3 4 5

    $month
     [1] "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov" "Dec"

    $df
         [,1] [,2]
    [1,]    1    4
    [2,]    2    5
    [3,]    3    6
```
使用names()可以查看和更改list的名称。list的length()返回的是names()的长度，而且由于list本身recursive的性质，对其进行算术运算往往是无意义的。
```r
    > names(x)
    [1] ""      "month" "df"  #没有预先指定的话，预设为空字符串
```
##索引
Index list时的基本手段仍然等同于vector，但我们往往关心的是list中某一项下的具体内容。而对list来说，[]返回的依然是一个list！  
只有**[[]] 或者 $**才能返回下一级的内容！
```r
    > x[1]
    [[1]]
    [1] 2 3 4 5
    > x[[2]]
     [1] "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov" "Dec"
    > x$mon #不需要打出完整名字
     [1] "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov" "Dec"
    > x[['month']]
     [1] "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov" "Dec"
```
涉及到list中不存在的位置时，结果与index方式有关。在index之前一定要小心。  
```r
    > x[4]
    $<NA>  #创建了新的项目
    NULL
    > x[[4]] #报错
    Error in x[[4]] : subscript out of bounds
    > x$days # 也创建了新的项目
    NULL
```
##转换
只有在特定条件下list才能和vector相互转化。

##增加和删除
使用**c()**可以直接合并两个list。new_list <- c(list1, list2)。如果有一个参数是vector，会先强制转换为list。使用cbind和rbind会产生不可预期的结果。
在list创建时，可以预先设定 list(some_name = NULL)，从而预先留下空位。  
一旦创建完毕，list[some_name] <- NULL 的作用是删除some_name这一项。如果一定要留空的话，应当是 list[some_name] <-  list(NULL)。注意是**[] 不是 [[]]** !!!!!
```r
    > x[1] = list(NULL) #创建后再修改
    > x
    [[1]]
    NULL
    $month
     [1] "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov" "Dec"
    $df
         [,1] [,2]
    [1,]    1    4
    [2,]    2    5
    [3,]    3    6
```
