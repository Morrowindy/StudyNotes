# 《Learning R》笔记 Chapter 5 下 dataframe

dataframe是R的特色数据结构之一。它相当于matrix + list，因此二者的很多性质也直接继承了过来。

## 创建
dataframe创建的基本格式依然是 data.frame(col_names = col_values) , 这一点类似于list。如果不特异指定rownames的话，第一个含有names的column将成为这个df的命名者。但我们也可以用row.names(df) <- NULL 或 某vector来指定名称或将名称清零。

由于继承了matrix的性质，因此**colnames() rownames() dimnames() ncol() nrow()** 这些函数也都适用于dataframe。而由于继承了list的性质，length()和names()对于dataframe来说相当于ncol()和colnames() .

在构建dataframe时，不同的column可以长度不同，但要求很苛刻，实际使用时应尽量避免。

## 索引
dataframe可以同时使用matrix和list风格的索引。但索引的输出结果要注意一下type：

```r
    > class(iris[1]) #输出的依然是个dataframe
    [1] "data.frame" #这里是list的语法
    > class(iris[,1])
    [1] "numeric"
    > class(iris[[1]])
    [1] "numeric"
    > class(iris$Sepal.Length)
    [1] "numeric"

subset()也能在dataframe中进行筛选，输出一个新的dataframe。它的基本格式是：
>subset(
dataframe_name,
              subset,#逻辑vector，用于筛选rows
              select # 表达式，用于筛选columns
)

    > subset(airquality, Day==1,select = Ozone:Wind) 
    #也可以直接写airquality, Day==1,Ozone:Wind
        Ozone Solar.R Wind
    1      41     190  7.4
    32     NA     286  8.6
    62    135     269  4.1
    93     39      83  6.9
    124    96     167  6.9
```
## 操作
dataframe可以使用t()转置。
rbind和cbind()也适用于dataframe。但rbind必须二者的names能够一一对应，否则报错。cbind则直接结合，但也要注意nrow是否一致。
```r
    > x=data.frame(x=1:3,y=2:4,z=3:5)
    > y=data.frame(y=0:2,z=4:6,t=5:7)
    > rbind(x,y)
    Error in match.names(clabs, names(xi)) : 名字同原来已有的名字不相对
    > p=data.frame(a=1:4,b=2:5,c=3:6)
    > cbind(x,p)
    Error in data.frame(..., check.names = FALSE) : 
      参数值意味着不同的行数: 3, 4
 ```

R自带的merge()能够合并两个dataframe。具体的语法可参考文档。它的基本格式是：
```r
    > merge(df_x, df_y,
    by.x = col_name_x , by.y = col_name_y , 
    all = TRUE
    ) 
```
