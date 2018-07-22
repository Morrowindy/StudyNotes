# 《Learning R》笔记 Chapter 4 下 matrix

Array是R中的2维或多维数据结构，matrix是使用最多的二维数据结构。
## 创建 
```r
    > a <- matrix( #这里使用array()也可以
    +             1:12, #原始vector，如果长度不够填满矩阵的话会用NA补足
    +             nrow = 4, 
    +             dimnames = list( #用list输入名称，可以看到首先是rowname，然后是colname
    +                 c('one','two','three','four'),
    +                 c('A','B','C')
    #byrow = FALSE 否则填充时按照row的方向
    +             ))
    > a
          A B  C
    one   1 5  9
    two   2 6 10
    three 3 7 11
    four  4 8 12
```
探索这个矩阵的结构也有一系列的函数**dim nrow ncol**,我们还能够利用dim()强制改变矩阵的形状。
```r
    > dim(a) ; nrow(a) ;ncol(a)
    [1] 4 3
    [1] 4
    [1] 3
    > dim(a) = c(2,6) #如果输入c(2,7)会报错 dims [product 14] do not match the length of object [12]
    > a
         [,1] [,2] [,3] [,4] [,5] [,6] #改变形状后原来的名称丢失
    [1,]    1    3    5    7    9   11
    [2,]    2    4    6    8   10   12 
    > length(a) #这里length()输出的依然是一维长度
    [1] 12
```
NROW和NCOL能够输出vector的维数而不报错。
colnames()和rownames()分别能够输出和改变矩阵的维度名称，也可以用dimnames()来修改，但输入必须是一个list。

##索引
索引matrix的基本方式是matrix[x,y]。在每一个维度内部索引的方式等同于vector。不同维度可以选用不同的索引方式。

##矩阵运算
要合并矩阵不能用**c()**，这样的运算方式只能把矩阵压缩成vector后再连接起来。
正确连接矩阵应使用**rbind() ; cbind()**.
相加的两个矩阵应当有相同形状，相乘的两个矩阵需要满足线代的形状要求。
**t()**可以转置矩阵。
%\*% 和 %o% 分别为内乘和外乘。
求逆不能使用 **^-1**， 而应使用solve()
eigen()可计算eigen值。

