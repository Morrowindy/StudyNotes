# 《Learning R》笔记 Chapter 6 上 环境

R中的环境（environment）和作用域（scope）使用list了这一数据结构，正如同python中使用对应的dict结构进行管理。  
当然环境本身不是list这一class/type，而是专门的environment class，可以用 **is.environment()** 进行判断。  
使用 **as.list和as.environment或list2env()** 能够相互转换。

创建一个新的envir，使用new.env()。新创建的env可以使用list的各种操作，如[[]]索引，$索引等。
在实际操作中，针对envir的赋值和取值，也会使用assign()和get()函数：
```r
    assign(x, value, pos = -1, envir = as.environment(pos), #x为变量名
       inherits = FALSE, immediate = TRUE) 
    
    get(x, pos = -1, envir = as.environment(pos), mode = "any",
    inherits = TRUE)
    #注意这里inherit默认是T，因此会在parent environment中也进行搜寻。
```
ls和ls.str能够接收env名称，输出其中的内容。exist()则是探究某环境中是否存在某变量名。
```r
    ls(envir=环境名)  ;  ls.str(envir=环境名） ; exist('变量名', 环境名)
    #exist(... ,  inherits = TRUE)类似get()
```
在R术语中，frame和environment是同义词。
**globalenv()** 储存控制台输入的变量；**baseenv()** 储存R的基础函数和变量：
```r
    > get('letters',envir = baseenv())
     [1] "a" "b" "c" "d" "e" "f" "g" "h" "i" "j" "k" "l" "m" "n" "o" "p" "q" "r" "s" "t" "u" "v" "w" "x"
    [25] "y" "z"
```
