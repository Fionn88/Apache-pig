# 猜題

## 各縣市警察局有幾個
> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);
foreach_police = FOREACH police GENERATE $0,SUBSTRING($2,0,3);
gp_police = GROUP foreach_police BY $1;
count_police = FOREACH gp_police GENERATE $0,COUNT($1);
dump colleage_police;

```
(南投縣,99)
(嘉義市,15)
(嘉義縣,87)
(基隆市,28)
(宜蘭縣,62)
(屏東縣,91)
(彰化縣,81)
(新北市,176)
(新竹市,19)
(新竹縣,61)
(桃園市,95)
(澎湖縣,28)
(臺中市,133)
(臺北市,107)
(臺南市,163)
(臺東縣,67)
(花蓮縣,73)
(苗栗縣,69)
(連江縣,7)
(金門縣,9)
(雲林縣,72)
(高雄市,153)
```

## 各縣市國小有幾間

> element = LOAD '/dataset/6087/6087.csv' Using PigStorage (',')  AS(code:chararray,school:chararray,city:chararray,address:chararray, phone:chararray,url:chararray);
foreach_element = FOREACH element GENERATE $1,$2;
gp_element = GROUP foreach_element BY $1;
count_element = FOREACH gp_element GENERATE $0,COUNT($1);
dump count_element;

```
(南投縣,139)
(嘉義市,20)
(嘉義縣,124)
(基隆市,42)
(宜蘭縣,76)
(屏東縣,168)
(彰化縣,175)
(新北市,216)
(新竹市,34)
(新竹縣,86)
(桃園市,190)
(澎湖縣,37)
(臺中市,236)
(臺北市,151)
(臺南市,211)
(臺東縣,88)
(花蓮縣,103)
(苗栗縣,114)
(連江縣,7)
(金門縣,19)
(雲林縣,155)
(高雄市,242)
```

## 各縣市平均一所小學有幾所警察局

> element = LOAD '/dataset/6087/6087.csv' Using PigStorage (',')  AS(code:chararray,school:chararray,city:chararray,address:chararray, phone:chararray,url:chararray);
foreach_element = FOREACH element GENERATE $1,$2;
gp_element = GROUP foreach_element BY $1;
count_element = FOREACH gp_element GENERATE $0,COUNT($1);

> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);
foreach_police = FOREACH police GENERATE $0,SUBSTRING($2,0,3);
gp_police = GROUP foreach_police BY $1;
count_police = FOREACH gp_police GENERATE $0,COUNT($1);

> join_element_police = JOIN count_element BY $0,count_police BY $0;
element_police = FOREACH join_element_police GENERATE $0,$1,$3;
per_school = FOREACH element_police GENERATE $0, ROUND_TO((double)$2/$1,2);
dump per_school

```
(南投縣,0.71)
(嘉義市,0.75)
(嘉義縣,0.7)
(基隆市,0.67)
(宜蘭縣,0.82)
(屏東縣,0.54)
(彰化縣,0.46)
(新北市,0.81)
(新竹市,0.56)
(新竹縣,0.71)
(桃園市,0.5)
(澎湖縣,0.76)
(臺中市,0.56)
(臺北市,0.71)
(臺南市,0.77)
(臺東縣,0.76)
(花蓮縣,0.71)
(苗栗縣,0.61)
(連江縣,1.0)
(金門縣,0.47)
(雲林縣,0.46)
(高雄市,0.63)
```

## 各縣市幼兒園有幾間

> kid = LOAD '/dataset/6086/6086.csv' Using PigStorage (',')  AS(code:chararray,school:chararray,city:chararray,address:chararray, phone:chararray);
foreach_kid= FOREACH kid GENERATE $1,$2;
gp_kid = GROUP foreach_kid BY $1;
count_kid = FOREACH gp_kid GENERATE $0,COUNT($1);
dump count_kid;

```
(南投縣,184)
(嘉義市,69)
(嘉義縣,153)
(基隆市,107)
(宜蘭縣,124)
(屏東縣,289)
(彰化縣,370)
(新北市,1134)
(新竹市,161)
(新竹縣,237)
(桃園市,584)
(澎湖縣,27)
(臺中市,737)
(臺北市,689)
(臺南市,565)
(臺東縣,122)
(花蓮縣,135)
(苗栗縣,182)
(連江縣,5)
(金門縣,26)
(雲林縣,146)
(高雄市,674)
```

## 各縣市平均一所幼稚園有幾所警察局

> kid = LOAD '/dataset/6086/6086.csv' Using PigStorage (',')  AS(code:chararray,school:chararray,city:chararray,address:chararray, phone:chararray);
foreach_kid= FOREACH kid GENERATE $1,$2;
gp_kid = GROUP foreach_kid BY $1;
count_kid = FOREACH gp_kid GENERATE $0,COUNT($1);

> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);
foreach_police = FOREACH police GENERATE $0,SUBSTRING($2,0,3);
gp_police = GROUP foreach_police BY $1;
count_police = FOREACH gp_police GENERATE $0,COUNT($1);

> join_kid_police = JOIN count_kid BY $0,count_police BY $0;
kid_police = FOREACH join_kid_police GENERATE $0,$1,$3;
per_kid = FOREACH kid_police GENERATE $0, ROUND_TO((double)$2/$1,2);
dump per_kid;

```
(南投縣,0.54)
(嘉義市,0.22)
(嘉義縣,0.57)
(基隆市,0.26)
(宜蘭縣,0.5)
(屏東縣,0.31)
(彰化縣,0.22)
(新北市,0.16)
(新竹市,0.12)
(新竹縣,0.26)
(桃園市,0.16)
(澎湖縣,1.04)
(臺中市,0.18)
(臺北市,0.16)
(臺南市,0.29)
(臺東縣,0.55)
(花蓮縣,0.54)
(苗栗縣,0.38)
(連江縣,1.4)
(金門縣,0.35)
(雲林縣,0.49)
(高雄市,0.23)
```

## 各縣市大學生有幾間

> colleage = LOAD '/dataset/9621/9621.csv' Using PigStorage (',')  AS(city:chararray,school:chararray,faculty:chararray,courses:chararray,level:chararray,student:int,teachers:int);
foreach_colleage = FOREACH colleage GENERATE $0,$1;
gp_colleage = GROUP foreach_colleage BY $0;
count_colleage = FOREACH gp_colleage GENERATE $0,COUNT($1);
dump count_colleage;

```
(南投縣,115)
(嘉義市,155)
(嘉義縣,263)
(基隆市,149)
(宜蘭縣,126)
(屏東縣,334)
(彰化縣,356)
(新北市,1039)
(新竹市,456)
(新竹縣,130)
(桃園市,708)
(澎湖縣,22)
(臺中市,1324)
(臺北市,2072)
(臺南市,966)
(臺東縣,70)
(花蓮縣,202)
(苗栗縣,148)
(金門縣,41)
(雲林縣,209)
(高雄市,1196)
```

## 各縣市平均一所大專院校有幾所警察局

> colleage = LOAD '/dataset/9621/9621.csv' Using PigStorage (',')  AS(city:chararray,school:chararray,faculty:chararray,courses:chararray,level:chararray,student:int,teachers:int);
foreach_colleage = FOREACH colleage GENERATE $0,$1;
gp_colleage = GROUP foreach_colleage BY $0;
count_colleage = FOREACH gp_colleage GENERATE $0,COUNT($1);

> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);
foreach_police = FOREACH police GENERATE $0,SUBSTRING($2,0,3);
gp_police = GROUP foreach_police BY $1;
count_police = FOREACH gp_police GENERATE $0,COUNT($1);

> join_colleage_police = JOIN count_colleage BY $0,count_police BY $0;
colleage_police = FOREACH join_colleage_police GENERATE $0,$1,$3;
per_colleage = FOREACH colleage_police GENERATE $0, ROUND_TO((double)$2/$1,2);
dump per_colleage;

```
(南投縣,0.86)
(嘉義市,0.1)
(嘉義縣,0.33)
(基隆市,0.19)
(宜蘭縣,0.49)
(屏東縣,0.27)
(彰化縣,0.23)
(新北市,0.17)
(新竹市,0.04)
(新竹縣,0.47)
(桃園市,0.13)
(澎湖縣,1.27)
(臺中市,0.1)
(臺北市,0.05)
(臺南市,0.17)
(臺東縣,0.96)
(花蓮縣,0.36)
(苗栗縣,0.47)
(金門縣,0.22)
(雲林縣,0.34)
(高雄市,0.13)
```

## 各縣市學生老師比

> colleage = LOAD '/dataset/9621/9621.csv' Using PigStorage (',')  AS(city:chararray,school:chararray,faculty:chararray,courses:chararray,level:chararray,student:int,teachers:int);
gp_colleage = GROUP colleage BY $0;
sum_colleage = FOREACH gp_colleage GENERATE $0, SUM($1.$5),SUM($1.$6);
foreach_colleage = FOREACH sum_colleage GENERATE $0, ROUND_TO((double)$1/$2,2);
dump foreach_colleage;

```
(南投縣,25.01)
(嘉義市,25.52)
(嘉義縣,24.53)
(基隆市,23.66)
(宜蘭縣,22.5)
(屏東縣,28.77)
(彰化縣,28.7)
(新北市,31.35)
(新竹市,22.37)
(新竹縣,31.66)
(桃園市,26.62)
(澎湖縣,24.46)
(臺中市,30.13)
(臺北市,24.95)
(臺南市,26.27)
(臺東縣,22.89)
(花蓮縣,18.78)
(苗栗縣,29.3)
(金門縣,30.21)
(雲林縣,29.03)
(高雄市,27.76)
```

## 各部別的一個老師分別負責幾個學生

> colleage = LOAD '/dataset/9621/9621.csv' Using PigStorage (',')  AS(city:chararray,school:chararray,faculty:chararray,courses:chararray,level:chararray,student:int,teachers:int);
gp_colleage = GROUP colleage BY $3;
sum_colleage = FOREACH gp_colleage GENERATE $0, SUM($1.$5),SUM($1.$6);
foreach_colleage = FOREACH sum_colleage GENERATE $0, ROUND_TO((double)$1/$2,2);
dump foreach_colleage;

```
(修,505.74)
(日,22.69)
(職,1094.08)
(P進,747.8)
```

## 各部別學生老師比例

> colleage = LOAD '/dataset/9621/9621.csv' Using PigStorage (',')  AS(city:chararray,school:chararray,faculty:chararray,courses:chararray,level:chararray,student:int,teachers:int);
gp_colleage = GROUP colleage BY $3;
sum_colleage = FOREACH gp_colleage GENERATE $0, SUM($1.$5),SUM($1.$6);
a = FOREACH sum_colleage GENERATE $0,ROUND_TO((double)$1/(($1+$2)*0.01),2), ROUND_TO((double)$2/(($1+$2)*0.01),2);

```
(修,99.8,0.2)
(日,95.78,4.22)
(職,99.91,0.09)
(P進,99.87,0.13)
```

## 各部門有關資訊管理及資訊工程學生與老師數量

> colleage = LOAD '/dataset/9621/9621.csv' Using PigStorage (',')  AS(city:chararray,school:chararray,faculty:chararray,courses:chararray,level:chararray,student:int,teachers:int);
filter_colleage = FILTER colleage BY $2 matches '資訊管理.*' OR $2 matches '資訊工程.*';
gp_colleage = GROUP filter_colleage BY $3;
sum_colleage = FOREACH gp_colleage GENERATE $0, SUM($1.$5), SUM($1.$6);
dump sum_colleage;

```
(修,7519,17)
(日,60867,2327)
(職,2278,0)
(P進,1219,0)
```

## 資訊開頭的科系，學士、碩士、博士、五專、二技 學生/老師比例

> colleage = LOAD '/dataset/9621/9621.csv' Using PigStorage (',')  AS(city:chararray,school:chararray,faculty:chararray,courses:chararray,level:chararray,student:int,teachers:int);
filter_colleage = FILTER colleage BY $2 matches '資訊.*';
gp_colleage = GROUP filter_colleage BY $4;
sum_colleage = FOREACH gp_colleage GENERATE $0, SUM($1.$5), SUM($1.$6);
percent_colleage = FOREACH sum_colleage GENERATE $0,ROUND_TO((double)$1/(($1+$2)*0.01),2), ROUND_TO((double)$2/(($1+$2)*0.01),2);
dump percent_colleage;

```
(博士,100.0,0.0)
(四技,96.62,3.38)
(學士,95.96,4.04)
(碩士,99.47,0.53)
(2二專,98.28,1.72)
(5五專,98.9,1.1)
(C二技,100.0,0.0)
(,0.0,100.0)
```

## 縣市部別的學生與老師的比例

> colleage = LOAD '/dataset/9621/9621.csv' Using PigStorage (',') AS(city:chararray,school:chararray,faculty:chararray,courses:chararray,level:chararray,student:int,teachers:int);
filter_colleage = FILTER colleage BY $3 == '修';
gp_colleage = GROUP filter_colleage BY $0;
sum_colleage = FOREACH gp_colleage GENERATE $0, SUM($1.$5),SUM($1.$6);
a = FOREACH sum_colleage GENERATE $0,ROUND_TO((double)$1/(($1+$2)*0.01),2), ROUND_TO((double)$2/(($1+$2)*0.01),2);

```
(南投縣,修,100.0,0.0)
(嘉義市,修,99.66,0.34)
(嘉義縣,修,99.91,0.09)
(基隆市,修,100.0,0.0)
(宜蘭縣,修,,)
(屏東縣,修,99.7,0.3)
(彰化縣,修,99.67,0.33)
(新北市,修,99.91,0.09)
(新竹市,修,99.93,0.07)
(新竹縣,修,99.84,0.16)
(桃園市,修,99.87,0.13)
(澎湖縣,修,100.0,0.0)
(臺中市,修,99.9,0.1)
(臺北市,修,99.81,0.19)
(臺南市,修,99.81,0.19)
(臺東縣,修,100.0,0.0)
(花蓮縣,修,99.02,0.98)
(苗栗縣,修,99.01,0.99)
(雲林縣,修,99.88,0.12)
(高雄市,修,99.72,0.28)
```

> filter_colleage = FILTER colleage BY $3 == '日';
gp_colleage = GROUP filter_colleage BY $0;
sum_colleage = FOREACH gp_colleage GENERATE $0, SUM($1.$5),SUM($1.$6);
a = FOREACH sum_colleage GENERATE $0,ROUND_TO((double)$1/(($1+$2)*0.01),2), ROUND_TO((double)$2/(($1+$2)*0.01),2);

```
(南投縣,日,95.65,4.35)
(嘉義市,日,95.34,4.66)
(嘉義縣,日,95.37,4.63)
(基隆市,日,95.48,4.52)
(宜蘭縣,日,95.5,4.5)
(屏東縣,日,95.97,4.03)
(彰化縣,日,95.78,4.22)
(新北市,日,96.29,3.71)
(新竹市,日,95.23,4.77)
(新竹縣,日,95.52,4.48)
(桃園市,日,95.61,4.39)
(澎湖縣,日,95.57,4.43)
(臺中市,日,96.11,3.89)
(臺北市,日,95.68,4.32)
(臺南市,日,95.67,4.33)
(臺東縣,日,95.19,4.81)
(花蓮縣,日,94.52,5.48)
(苗栗縣,日,96.1,3.9)
(金門縣,日,95.99,4.01)
(雲林縣,日,96.08,3.92)
(高雄市,日,95.7,4.3)
```

> filter_colleage = FILTER colleage BY $3 == '職';
gp_colleage = GROUP filter_colleage BY $0;
sum_colleage = FOREACH gp_colleage GENERATE $0, SUM($1.$5),SUM($1.$6);
a = FOREACH sum_colleage GENERATE $0,ROUND_TO((double)$1/(($1+$2)*0.01),2), ROUND_TO((double)$2/(($1+$2)*0.01),2);

```
(南投縣,職,100.0,0.0)
(嘉義市,職,100.0,0.0)
(嘉義縣,職,100.0,0.0)
(基隆市,職,99.84,0.16)
(宜蘭縣,職,100.0,0.0)
(屏東縣,職,99.5,0.5)
(彰化縣,職,100.0,0.0)
(新北市,職,100.0,0.0)
(新竹市,職,99.93,0.07)
(新竹縣,職,100.0,0.0)
(桃園市,職,99.95,0.05)
(澎湖縣,職,100.0,0.0)
(臺中市,職,99.97,0.03)
(臺北市,職,99.92,0.08)
(臺南市,職,99.75,0.25)
(臺東縣,職,100.0,0.0)
(花蓮縣,職,100.0,0.0)
(苗栗縣,職,100.0,0.0)
(金門縣,職,100.0,0.0)
(雲林縣,職,99.09,0.91)
(高雄市,職,99.92,0.08)
```

> filter_colleage = FILTER colleage BY $3 == 'P進';
gp_colleage = GROUP filter_colleage BY $0;
sum_colleage = FOREACH gp_colleage GENERATE $0, SUM($1.$5),SUM($1.$6);
a = FOREACH sum_colleage GENERATE $0,ROUND_TO((double)$1/(($1+$2)*0.01),2), ROUND_TO((double)$2/(($1+$2)*0.01),2);

```
(嘉義市,P進,100.0,0.0)
(嘉義縣,P進,100.0,0.0)
(基隆市,P進,100.0,0.0)
(宜蘭縣,P進,100.0,0.0)
(屏東縣,P進,100.0,0.0)
(彰化縣,P進,100.0,0.0)
(新北市,P進,99.85,0.15)
(新竹市,P進,99.86,0.14)
(桃園市,P進,99.82,0.18)
(臺中市,P進,99.84,0.16)
(臺北市,P進,99.78,0.22)
(臺南市,P進,100.0,0.0)
(臺東縣,P進,100.0,0.0)
(苗栗縣,P進,99.37,0.63)
(金門縣,P進,100.0,0.0)
(高雄市,P進,100.0,0.0)
```

## 請問臺北市所有大學資訊工程系人數

> colleage = LOAD '/dataset/9621/9621.csv' Using PigStorage (',') AS(city:chararray,school:chararray,faculty:chararray,courses:chararray,level:chararray,student:int,teachers:int);
filter_colleage = FILTER colleage BY $0 == '臺北市' AND $2 matches '資訊工程.*';
gp_colleage = GROUP filter_colleage BY $0;
sum_colleage = FOREACH gp_colleage GENERATE $0, SUM($1.$5)+SUM($1.$6);
dump sum_colleage;

```
(臺北市,4948)
```

## 資訊開頭的科系，各部門老師平均一人負責幾個學生

> colleage = LOAD '/dataset/9621/9621.csv' Using PigStorage (',')  AS (city:chararray,school:chararray,faculty:chararray,courses:chararray,level:chararray,student:int,teachers:int);
filter_colleage = FILTER colleage BY $2 matches '資訊.*';
gp_colleage = GROUP filter_colleage BY $3;
sum_colleage = FOREACH gp_colleage GENERATE $0, ROUND_TO((double)SUM($1.$5)/SUM($1.$6),2);
dump sum_colleage;

```
(修,464.55)
(日,26.24)
(職,)
(P進,)
```