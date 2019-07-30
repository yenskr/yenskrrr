---
title: split one column to two columns2
author: ''
date: '2019-07-30'
slug: split-one-column-to-two-columns2
categories: []
tags:
  - R
  - tidyr
  - data wrangling
images: []
---

## Preface

清理資料的時候，常常會需要用到`dplyr`套件裡`mutate`、`group_by`、`summarise`等函式（`dplyr`跟pipeline運算子`%>%`應該是每個初學R做資料分析的人必學的套件吧，~~沒學過不要說你會R~~）。

今天除了紀錄一下在解實際問題時個人的思路解法，還會介紹一個`tidyr`套件的函式，有需要的朋友可以參考看看。

## Context

最近收到一份資料，其中有個欄位像這樣:
``` r
> head(df$GPS)
[1] "22.627126,120.312473" "22.624569,120.360211"
[3] "22.611157,120.329407" "22.657952,120.324472"
```
需求很簡單，就是把`df`的`GPS`欄位拆開成`LNG`,`LAT`兩個欄位。

## Problem
> 把一個 data frame 的欄位切開成兩個欄位

## Solution1：using base function

先記錄一下自己使用基本函式的解法思路

1. 使用`strsplit`把資料分開
    ```
    > strsplit(dt$發生地點GPS, ',')
    [[1]]
    [1] "22.627126"  "120.312473"
    [[2]]
    [1] "22.624569"  "120.360211"
    [[3]]
    [1] "22.611157"  "120.329407"
    [[4]]
    [1] "22.657952"  "120.324472"
    [[5]]
    [1] "22.639282"  "120.330766"
    [[6]]
    [1] "22.641744"  "120.313873"
    ```
2. 可以發現雖然成功切開，不過變成 List of lists 的形式
3. 這時我們只要善用`sapply`搭配`[`就可以取出每個list中的第1個元素
4. 搭配`mutate`的效果：
    ```
    > dt %>% mutate(
        lat=sapply(strsplit(dt$發生地點GPS,','),"[",1),
        lng=sapply(strsplit(dt$發生地點GPS,','),"[",2)
      ) %>% select(lat,lng)
    # A tibble: 2,790 x 2
       lat       lng       
       <chr>     <chr>     
     1 22.627126 120.312473
     2 22.624569 120.360211
     3 22.611157 120.329407
     4 22.657952 120.324472
     5 22.639282 120.330766
     6 22.641744 120.313873
     7 22.644323 120.298523
     8 22.647354 120.314703
     9 22.633798 120.313527
    10 22.633798 120.313527
    # ... with 2,780 more rows
    ```

## Solution2：using `tidyr::seperate`

後來在找相關資料的時候，找到了`tidyr`的`seperate`，直接一行搞定。

`seperate {tidyr}`的`help document`標題寫得很清楚：

> Separate a character column into multiple columns using a regular expression separator.

實際操作試試看
``` r
> dt %>% separate(發生地點GPS, c("lat", "lng"),sep=',') %>% select(lat,lng)
# A tibble: 2,790 x 2
   lat       lng       
   <chr>     <chr>     
 1 22.627126 120.312473
 2 22.624569 120.360211
 3 22.611157 120.329407
 4 22.657952 120.324472
 5 22.639282 120.330766
 6 22.641744 120.313873
 7 22.644323 120.298523
 8 22.647354 120.314703
 9 22.633798 120.313527
10 22.633798 120.313527
# ... with 2,780 more rows
```

還有很多延伸的用法，有機會再來研究。

## Reference
* https://tidyr.tidyverse.org/reference/separate.html
* https://stackoverflow.com/questions/4350440/split-data-frame-string-column-into-multiple-columns

###### tags: `R` `tidyr` `data wrangling`