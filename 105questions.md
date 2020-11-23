# 105模擬題目
## 999004 - 使用者個人資料
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
```
欄位名稱
使用者id userid chararray
性別  gender chararray
年齡  age int
國家  country chararray
註冊時間 registered chararray
```

### 會員年齡層分布，第一個欄位請一定依照下方樣式輸出
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_userprofile = FILTER userprofile BY $2 < 20;
gp_userprofile = GROUP filter_userprofile ALL;
count_userprofile = FOREACH gp_userprofile GENERATE $0,COUNT($1);
dump count_userprofile;
```
(all,44)
```

> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_userprofile = FILTER userprofile BY $2 > 19 AND NOT $2 > 39;
gp_userprofile = GROUP filter_userprofile ALL;
count_userprofile = FOREACH gp_userprofile GENERATE $0,COUNT($1);
dump count_userprofile;
```
(all,256)
```

> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_userprofile = FILTER userprofile BY $2 > 39 AND NOT $2 > 64;
gp_userprofile = GROUP filter_userprofile ALL;
count_userprofile = FOREACH gp_userprofile GENERATE $0,COUNT($1);
dump count_userprofile;
```
(all,14)
```
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_userprofile = FILTER userprofile BY $2 > 64;
gp_userprofile = GROUP filter_userprofile ALL;
count_userprofile = FOREACH gp_userprofile GENERATE $0,COUNT($1);
dump count_userprofile;
```
(all,5)

Ans:
(0-19,44)
(20-39,256)
(40-64,14)
(65--,5)
```


## 999005 - 使用者點聽紀錄
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
```
欄位名稱
使用者id  userid chararray
點聽時間  time chararray
歌手名稱  artname chararray
歌曲名稱  traname chararray
```

### 那一天是會員透過我們的音樂網站聆聽音樂最多的一天 ?
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
sub_userdemand = FOREACH userdemand GENERATE SUBSTRING($1,0,10),$2,$3;
gp_userdemand = GROUP sub_userdemand BY $0;
count_userdemand = FOREACH gp_userdemand GENERATE $0,COUNT($1);
asc_userdemand = ORDER count_userdemand BY $1 ASC;
dump asc_userdemand;
```
(2008-09-24,250)
```

## 999004 跟 999005 均會用到
### 男性與女性的會員數量與總點播次數
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
join1 = JOIN userdemand BY $0, userprofile BY $0;
gp_userprofile = GROUP join1 BY $5;
count_userprofile = FOREACH gp_userprofile GENERATE $0, COUNT($1);
dump count_userprofile;
```
(f,52636)
(m,102146)
```

> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
gp_userprofile = GROUP userprofile BY $1;
count_userprofile = FOREACH gp_userprofile GENERATE $0, COUNT($1);
dump count_userprofile;
```
(f,137)
(m,182)

Ans:
(f,137,52636)
(m,182,102146)
```

### 會員數量排行顯示前五名的國家，和這些國家的總點播次數
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
join1 = JOIN userdemand BY $0, userprofile BY $0;
gp_userprofile1 = GROUP join1 BY $7;
count_userprofile1 = FOREACH gp_userprofile1 GENERATE $0, COUNT($1);
dump count_userprofile1;
```
(Canada,37110)
(France,1618)
(Greece,192)
(Latvia,727)
(Mexico,2991)
(Norway,3649)
(Poland,10664)
(Serbia,994)
(Sweden,3147)
(Turkey,10707)
(Armenia,584)
(Belgium,2967)
(Croatia,1237)
(Estonia,339)
(Finland,8409)
(Germany,14558)
(Hungary,1572)
(Ireland,1480)
(Morocco,587)
(Romania,1265)
(Bulgaria,364)
(Portugal,1454)
(Slovakia,1689)
(Thailand,372)
(Argentina,3096)
(Australia,1760)
(Nicaragua,44)
(Venezuela,950)
(Netherlands,468)
(New Zealand,340)
(Switzerland,1769)
(United States,9255)
(Czech Republic,1673)
(United Kingdom,2092)
(Russian Federation,2348)
(Trinidad and Tobago,3223)
(Canada Minor Outlying Islands,1089)
(British Indian Ocean Territory,649)
```

> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
gp_userprofile2 = GROUP userprofile BY $3;
count_userprofile2 = FOREACH gp_userprofile2 GENERATE $0, COUNT($1);
asc_userprofile2 = ORDER count_userprofile2 BY $1;
dump asc_userprofile2;
```
(Canada,60)
(Germany,35)
(China,34)
(Taiwan,20)
(Poland,19)
(Turkey,14)
(United States,12)
(Finland,10)
```

> join12 = JOIN count_userprofile1 BY $0,count_userprofile2 BY $0;
foreach_join12 = FOREACH join12 GENERATE $0,$3,$1;
asc_join12 = ORDER foreach_join12 BY $1 ASC;
dump asc_join12;
```
(United States,12,9255)
(Turkey,14,10707)
(Poland,19,10664)
(Germany,35,14558)
(Canada,60,37110)
```