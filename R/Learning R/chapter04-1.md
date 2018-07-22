# 《Learning R》笔记 Chapter 4 上 Vector

本章开始介绍R中的数据类型：vector matrix array。 本篇总结vector  

## Vector
###创建
vector是R中最基本的一维数据结构。要创造出某个特定class的vector，我们可以使用这样的命令：**vector（‘class/type’ , length）** :
```r
    > vector('character' , 10)
     [1] "" "" "" "" "" "" "" "" "" ""
    > vector('logical' , 10)
     [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE #注意全是false
    > vector('list' , 2) #对list来说唯一可用的syntax，不能简化！
    [[1]]
    NULL

    [[2]]
    NULL
 ```
简化的写法可以用**logical(10)** 。但这种方法只能用在atomic类型，如果用于list，例如list(2)，得到的另外结果。  
为了创造一个sequence，除了使用最简单的“ **:** ”之外，R中的原型函数为seq()，但实际用途中往往使用他的特化版 **seq.int ; seq_len ; seq_along** , 具体的参数如下：
```r
>seq.int(from, to, by, length.out, along.with, ...)
seq_along(along.with)
seq_len(length.out) #起始必定为1
```

>from和to分别是starting和(maximal)end value。by是increment。length.out是期望的length，along.with接受另一个vector，以这个vector的length作为length。
```r
    > seq.int(1  ,  3.4  ,  .22  )
     [1] 1.00 1.22 1.44 1.66 1.88 2.10 2.32 2.54 2.76 2.98 3.20 #只有起始是准确的
    > seq_len(4.55)
    [1] 1 2 3 4
```
###长度 命名
vector的长度用length()来获取。要获取一个字符串本身的长度，得用另一个函数**nchar()**
```r
    > nchar('Markdown') ; length('Markdown')
    [1] 8
    [1] 1
```
length()也可以被用来强行修改vector的长度（length(some_vector) <- new_length），但一般不推荐。长度改短时会截取，该长时会用NA填充。  

vector可以被赋予名字，默认的名字为**NULL**。names()函数既能够输出名字构成的字符串vector，也能够接受输入，更改名字。  
```r
    > c(a=2,b=4,'s.t'=0,3)
      a   b s.t     
      2   4   0   3 
```
###定位
R中vector的定位（indexing）也使用的是[ ]，但需要和python区分的是，R中的定位从1开始，而python从0开始。  
[ ]可以接受以下4中类型的vector输入，这4种类型**不能混用**：  
1. 正整数：输出位置为输入值的对应元素  
2. 负整数：输出位置为输入值**以外**的对应元素
3. 逻辑值（TRUE FALSE NA）：输出位置为TRUE的所有对应元素，如果index为NA则输出NA
4. 字符串：输出对应名称的元素.

在使用逻辑值时有两个容易出错的地方：
```r
    > x=1:5 ; x[c(TRUE,FALSE,NA)]
    [1]  1 NA  4 
    #可以看到，由于逻辑vector长度与原vector不匹配，这个逻辑vector被循环使用
    #因此在使用逻辑值时，最好保证长度一致
    > x <- c(2,3,4,5,NA,1,NA)
    > x[x>3]
    [1]  4  5 NA NA
    > x[which(x>3)]
    [1] 4 5
    > which(x>3)
    [1] 3 4
    #由于[NA]一定会给出NA，因此在处理有NA的数据时，最好用 which()

 >**which()**接收1个logical vector，返回1个integer vector，内容为原logical vector中TRUE的下标。
```
##重复
正如前面的笔记所说，不同长度的vector在进行运算时，较短的那个会被循环使用，可能会产生warning和难以预料的结果，应当尽量避免。  
要手动进行可控的重复/循环，我们应使用rep()函数。
```r
>rep(x, ...)
rep.int(x, times)
rep_len(x, length.out)
... 
  times : an integer-valued vector giving the (non-negative) number of times to repeat each element if of length length(x), or to repeat the whole vector if of length 1. Negative or NA values are an error.  
  length.out : non-negative integer. The desired length of the output vector.
  each : non-negative integer. Each element of x is repeated each times.

    > rep(1:4,3) ; rep(1:4,each=3) ; rep_len(1:4,7)
     [1] 1 2 3 4 1 2 3 4 1 2 3 4
     [1] 1 1 1 2 2 2 3 3 3 4 4 4
    [1] 1 2 3 4 1 2 3
```
