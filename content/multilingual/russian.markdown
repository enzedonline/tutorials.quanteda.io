---
title: Russian
weight: 15
draft: false
---

{{% author %}}By Lana Bilalova{{% /author %}} 


```r
require(quanteda)
require(quanteda.corpora)
options(width = 110)
```

## Russian 

After tokenization, we remove so called "stopwords" using `stopwords("ru", source = "snowball")` or 
`stopwords("ru", source = "marimo")`. [Marimo](https://github.com/koheiw/marimo) is larger and better for multilingual analysis than Snowball. Please be very careful when pre-processing or removing tokens since these choices [might influence subsequent results](https://doi.org/10.1017/pan.2017.44). If you want tokens to comprise only of Cyrillic script, you can select them by `"^[а-яА-Я]+$"`.


```r
# reshape corpus to the level of paragraphs
corp_ru <- corpus_reshape(data_corpus_udhr["rus"], to = "paragraphs")

# tokenize corpus and apply pre-processing
toks_ru <- tokens(corp_ru, remove_punct = TRUE, remove_numbers = TRUE) %>% 
  tokens_remove(pattern = stopwords("ru", source = "snowball")) 
print(toks_ru[2], max_ndoc = 1, max_ntoken = -1)
```

```
## Tokens consisting of 1 document and 4 docvars.
## rus :
##   [1] "Принимая"          "внимание"          "признание"         "достоинства"       "присущего"        
##   [6] "всем"              "членам"            "человеческой"      "семьи"             "равных"           
##  [11] "неотъемлемых"      "прав"              "является"          "основой"           "свободы"          
##  [16] "справедливости"    "всеобщего"         "мира"              "принимая"          "внимание"         
##  [21] "пренебрежение"     "презрение"         "правам"            "человека"          "привели"          
##  [26] "варварским"        "актам"             "которые"           "возмущают"         "совесть"          
##  [31] "человечества"      "создание"          "такого"            "мира"              "котором"          
##  [36] "люди"              "будут"             "иметь"             "свободу"           "слова"            
##  [41] "убеждений"         "будут"             "свободны"          "страха"            "нужды"            
##  [46] "провозглашено"     "высокое"           "стремление"        "людей"             "принимая"         
##  [51] "внимание"          "необходимо"        "права"             "человека"          "охранялись"       
##  [56] "властью"           "закона"            "целях"             "обеспечения"       "вынужден"         
##  [61] "прибегать"         "качестве"          "последнего"        "средства"          "восстанию"        
##  [66] "против"            "тирании"           "угнетения"         "принимая"          "внимание"         
##  [71] "необходимо"        "содействовать"     "развитию"          "дружественных"     "отношений"        
##  [76] "народами"          "принимая"          "внимание"          "народы"            "Объединенных"     
##  [81] "Наций"             "подтвердили"       "Уставе"            "веру"              "основные"         
##  [86] "права"             "человека"          "достоинство"       "ценность"          "человеческой"     
##  [91] "личности"          "равноправие"       "мужчин"            "женщин"            "решили"           
##  [96] "содействовать"     "социальному"       "прогрессу"         "улучшению"         "условий"          
## [101] "жизни"             "большей"           "свободе"           "принимая"          "внимание"         
## [106] "государства-члены" "обязались"         "содействовать"     "сотрудничестве"    "Организацией"     
## [111] "Объединенных"      "Наций"             "всеобщему"         "уважению"          "соблюдению"       
## [116] "прав"              "человека"          "основных"          "свобод"            "принимая"         
## [121] "внимание"          "всеобщее"          "понимание"         "характера"         "этих"             
## [126] "прав"              "свобод"            "имеет"             "огромное"          "значение"         
## [131] "полного"           "выполнения"        "обязательства"     "Генеральная"       "Ассамблея"        
## [136] "провозглашает"     "настоящую"         "Всеобщую"          "декларацию"        "прав"             
## [141] "человека"          "качестве"          "задачи"            "выполнению"        "которой"          
## [146] "должны"            "стремиться"        "народы"            "государства"       "каждый"           
## [151] "каждый"            "орган"             "общества"          "постоянно"         "имея"             
## [156] "виду"              "настоящую"         "Декларацию"        "стремились"        "путем"            
## [161] "просвещения"       "образования"       "содействовать"     "уважению"          "этих"             
## [166] "прав"              "свобод"            "обеспечению"       "путем"             "национальных"     
## [171] "международных"     "прогрессивных"     "мероприятий"       "всеобщего"         "эффективного"     
## [176] "признания"         "осуществления"     "среди"             "народов"           "государств-членов"
## [181] "Организации"       "среди"             "народов"           "территорий"        "находящихся"      
## [186] "юрисдикцией"
```


```r
# construct a document-feature matrix
# note that now all the features are converted to lowercase by default
dfmat_ru <- dfm(toks_ru)
print(dfmat_ru)
```

```
## Document-feature matrix of: 82 documents, 648 features (98.19% sparse) and 4 docvars.
##        features
## docs    преамбула принимая внимание признание достоинства присущего всем членам человеческой семьи
##   rus.1         1        0        0         0           0         0    0      0            0     0
##   rus.2         0        7        7         1           1         1    1      1            2     1
##   rus.3         0        0        0         0           0         0    0      0            0     0
##   rus.4         0        0        0         0           0         0    0      0            0     0
##   rus.5         0        0        0         0           0         0    0      0            0     0
##   rus.6         0        0        0         0           0         0    0      0            0     0
## [ reached max_ndoc ... 76 more documents, reached max_nfeat ... 638 more features ]
```

