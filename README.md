長庚大學 大數據分析方法 作業三
================

-   用文字搭配程式碼解釋爬蟲結果
    -   共爬出幾篇文章標題？（程式碼與文字解釋各`5pt`）
        -   dim(), nrow(), str()皆可
    -   哪個作者文章數最多？（程式碼與文字解釋各`5pt`）
        -   table()
    -   其他爬蟲結果解釋（`10pt`）
        -   試著找出有趣的現象，不一定要用程式碼搭配解釋，也可只用文字

網站資料爬取
------------

``` r
library(xml2)
library(rvest) 
```

    ## Warning: package 'rvest' was built under R version 3.3.3

``` r
frame = data.frame(Title=character(),
                      Author=character(),
                      PushNum=character())
for(i in 4673:4675){
PTTURL<-paste0("https://www.ptt.cc/bbs/NBA/index",i,".html") 
PTTContent <- read_html(PTTURL)
post_title <- PTTContent %>% html_nodes(".title") %>% html_text() 
post_title <- gsub("\n",replacement="",post_title)
post_title <- gsub("\t",replacement="",post_title)
post_author<- PTTContent %>% html_nodes(".author") %>% html_text()
post_pushnum <- PTTContent %>% html_nodes(".nrec") %>% html_text()
PTTframe <- data.frame(Title = post_title, Author = post_author, PushNum = post_pushnum)
frame <- rbind(frame,PTTframe)
}
```

爬蟲結果呈現
------------

``` r
#這是R Code Chunk
knitr::kable(frame)
```

| Title                                            | Author       | PushNum |
|:-------------------------------------------------|:-------------|:--------|
| \[情報\] 西河破紀錄啦！！！！                    | ck0987515477 | 爆      |
| \[討論\] 恭喜龜龜破紀錄                          | ZaneTrout    | 11      |
| \[花邊\] Russell Westbrook本季42次大三元達成     | jay0601zzz   | 12      |
| \[BOX \] Thunder 106:105 Nuggets 數據            | Rambo        | 爆      |
| \[討論\] 龜龜絕殺50分超級大三元+單季42次大三元   | asonge0000   | 68      |
| \[討論\] 我到底看了三小???                       | RussellWestb | 26      |
| \[專欄\]哈登vs.衛少狹路相逢 火箭恐怕飛不起來LYS  | zzyyxx77     | X2      |
| \[心得\] 龜龜這場是雙絕殺!逆轉+對方季後賽out     | checktime    | 80      |
| \[情報\] 德佬例行賽場次超越TD                    | jay0601zzz   | 84      |
| \[討論\] 我龜MVP是不是穩了                       | kobeyoung    | 76      |
| \[BOX \] Pistons 103:90 Grizzlies 數據           | Rambo        | 6       |
| \[外絮\] Westbrook 破紀錄賽後球員推特祝賀        | hungys       | 59      |
| \[BOX \] Mavericks 111:124 Suns 數據             | Rambo        | 15      |
| \[BOX \] Rockets 135:128 Kings 數據              | Rambo        | 95      |
| \[外絮\] CJ和Lillard感謝龜龜：你是真正的MVP      | Ansel        | 63      |
| \[討論\] KD有冠的話應該會超越Dirk吧?             | siriusc      | 11      |
| \[討論\] Westbrook破紀錄的大三元助攻影片         | pttnowash    | 23      |
| \[新聞\] 這一球被吹犯畢業 詹皇龍顏大怒           | jay0601zzz   | 29      |
| \[Live\] 灰狼 @ 湖人                             | Rambo        | 43      |
| \[閒聊\] 騎士老鷹之戰的一些記錄                  | dragon803    | 16      |
| \[情報\] 龜龜大三元次數正式超越張大帥            | sthho        | 28      |
| \[發錢\] 當代神獸雙破大三元                      | monmo        | 爆      |
| \[情報\] Russell Westbrook 大三元次數超越 Oscar  | gold97972000 | 17      |
| \[討論\] Westbrook是不是已經比KD強了             | FenixShou    | 60      |
| \[情報\] Kobe轉發西河今天的絕殺影片：還有疑問嗎? | tmacor1      | 76      |
| Re: \[新聞\]單季2次50分大三元 哈登史上第一人     | checktime    | 23      |
| \[祭品\] 哈登MVP!                                | konayuki     | X5      |
| \[新聞\] 詹姆斯大三元+厄文45分 騎士還是被逆轉    | KyrieIrving1 | 27      |
| \[新聞\] MVP給誰公平？布萊恩：丟硬幣決定         | zzyyxx77     | 14      |
| \[新聞\] 超遠三分絕殺幸運球？ 衛少：我不是亂投   | pneumo       | 14      |
| \[新聞\] 本季主場最終戰 太陽曬小牛圓滿收尾       | zzzz8931     | 1       |
| \[討論\] 湖人的防守還有救嗎?                     | tiffanycute  | 15      |
| \[討論\] 單季場均大三元+得分王                   | pptdog       | 20      |
| \[討論\] 冠軍跟大三元紀錄是否不可兼得?           | journeytou   | 17      |
| \[花邊\] MVP給誰公平？布萊恩：你們丟硬幣決定     | adam7148     | 6       |
| (本文已被刪除) \[ericl1234567\]                  | -            | 27      |
| \[討論\] Rose現在怎麼想？                        | sss631036    | 6       |
| Re: \[專欄\] 15項NBA最難破的紀錄                 | Howl7        | 35      |
| \[討論\] 騎士最近的比賽跟人事是不是都很謎？      | wmigrant     | 28      |
| Re: \[討論\] Rose現在怎麼想？                    | magicbook123 | X2      |
| \[情報\] MVP 賭盤風向吹更大了(鬍迷有福了)        | checktime    | 34      |
| Re: \[討論\] Westbrook是不是已經比KD強了         | ymgs1507     |         |
| \[外絮\] Gobert成1000/1000/200第12人             | monmo        | 32      |
| \[新聞\] 衛少奪MVP？　哈登：贏球才是MVP該做的事  | adam7148     | 爆      |
| \[外絮\] Bleacher report將龜龜比喻成快銀         | h1212123tw   | 23      |
| \[討論\] 場均大三元是不是RW生涯顛峰了            | supereight   | 25      |
| Re: \[討論\] 場均大三元是不是RW生涯顛峰了        | djviva       | 26      |
| \[討論\] 今年的騎士二連霸霸業誰能抵抗?           | transformer8 | X1      |
| \[討論\] 場均大三元有助於招募隊友?               | strmof22     | 9       |
| \[討論\] 如果西河拿MVP會是最弱MVP嗎？            | jessica805   | X2      |
| Re: \[討論\] 如果西河拿MVP會是最弱MVP嗎？        | sweetgold    | X1      |
| \[情報\] 五大數據各式紀錄保持者                  | MrSatan      | 25      |
| Re: \[討論\] Rose現在怎麼想？                    | ddrose       | 27      |
| \[討論\] 從2006/2008年MVP競爭看當季話題性的重要  | dro001       | 22      |
| \[情報\] 騎士的尷尬紀錄                          | saber154     | 19      |
| \[討論\] 重整隊伍該選Curry或Westbrook?           | lcall        | 60      |
| \[討論\] 集全隊之力，下一個可以刷的數據          | RuleAllWorld |         |
| \[討論\] 雷霆教練B.Donovan是不是很有料?          | qk56         | 12      |
| \[情報\] 小皇帝:我不覺得那是個犯規               | scott6065    | 16      |
| Re: \[討論\] 集全隊之力，下一個可以刷的數據      | sin17        |         |

解釋爬蟲結果
------------

``` r
str(frame)
```

    ## 'data.frame':    60 obs. of  3 variables:
    ##  $ Title  : Factor w/ 59 levels "[BOX ] Mavericks 111:124 Suns 數據",..: 17 14 9 4 15 12 16 6 18 13 ...
    ##  $ Author : Factor w/ 49 levels "Ansel","asonge0000",..: 4 13 7 10 2 11 14 3 7 8 ...
    ##  $ PushNum: Factor w/ 35 levels "11","12","15",..: 18 1 2 18 12 6 17 14 15 13 ...

``` r
table(frame$Author)
```

    ## 
    ##        Ansel   asonge0000    checktime ck0987515477    dragon803 
    ##            1            1            3            1            1 
    ##       hungys   jay0601zzz    kobeyoung    pttnowash        Rambo 
    ##            1            3            1            1            5 
    ## RussellWestb      siriusc    ZaneTrout     zzyyxx77            - 
    ##            1            1            1            2            1 
    ##     adam7148    FenixShou gold97972000        Howl7   journeytou 
    ##            2            1            1            1            1 
    ##     konayuki KyrieIrving1 magicbook123        monmo       pneumo 
    ##            1            1            1            2            1 
    ##       pptdog    sss631036        sthho  tiffanycute      tmacor1 
    ##            1            1            1            1            1 
    ##     wmigrant     zzzz8931       ddrose       djviva       dro001 
    ##            1            1            1            1            1 
    ##   h1212123tw   jessica805        lcall      MrSatan         qk56 
    ##            1            1            1            1            1 
    ## RuleAllWorld     saber154    scott6065        sin17     strmof22 
    ##            1            1            1            1            1 
    ##   supereight    sweetgold transformer8     ymgs1507 
    ##            1            1            1            1

1.63篇

2.checktime跟jay0601zzz 最多

``` r
#這是R Code Chunk
```

找不太到
