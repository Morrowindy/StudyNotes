# 《Learning R》笔记之 Preface & Chapter 1 寻求帮助

本书的前言部分提到的数据分析总体workflow可谓提纲挈领。所谓的**RCEMP**。在实际经验中Clean这一步往往是耗时最多的。   
1. **R**etrive some data  
2. **C**lean the data  
3. **E**xplore and visualize the data  
4. **M**odel the data and make predictions  
5. **P**resent or publish your results 
 
安装R和Rstudio后，我们开始正式使用R。
在命令行界面下, **?** 加函数名称 能够给出这个函数的详细介绍，等同于**help()**。**??**则可以搜索关键主题，等同于**help.search()**。但只限于本机已经安装的内容。

```r

?glm 等于 help('glm')      ??'linear regression' 等于 help.search('linear regression')  
注意?[ 是会报错的，必须用 ?'[' 或 help('[') 
```



使用**apropos()**可以返回一个charactor vector, 其元素能够匹配输入的string，返回符合要求的变量和函数名（换言之也接受正则表达式）。

```r
> glmm <- rnorm(20)
> apropos('glm')
[1] "glm"           "glm.control"   "glm.fit"       "glmm"          "predict.glm"   "residuals.glm" "summary.glm"  
> apropos('glm$')
[1] "glm"           "predict.glm"   "residuals.glm" "summary.glm"  
```

某些package还含有vignette，格式为html、pdf等。如果输入 


```r
browseVignettes() #会打开一个网页，列举本机所有的vignette
browseVignettes(package='knitr') #打开网页，列举knitr包中的9篇vignettes
```

而使用**RSiteSearch()**则能在网络上检索所有的R包。当然google和Stackoverflow也是很优秀的检索途径。
    
