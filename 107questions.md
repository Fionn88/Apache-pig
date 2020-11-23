# 107模擬題

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

### 請根據資料集，查詢出在目前會員人數男性與女性的會員人數分別是多少?
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
gp_userprofile = GROUP userprofile BY $1;
count_userprofile = FOREACH gp_userprofile GENERATE $0, COUNT($1);
dump count_userprofile;
```
(f,137)
(m,182)
```

### 請根據資料集查詢出每個國家的會員數量，並顯示前五名的國家與會員人數。
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
gp_profile = GROUP userprofile BY $3;
count_profile = FOREACH gp_profile GENERATE $0, COUNT($1);
desc_profile = ORDER count_profile BY $1 DESC;
limit_profile = LIMIT desc_profile 5;
dump limit_profile;
```
(Canada,60)
(Germany,35)
(China,34)
(Taiwan,20)
(Poland,19)
```

### 在會員資料表中，年紀在20至30歲的會員人數共有多少位？
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $2 > 20 AND NOT $2 > 30;
gp_profile = GROUP filter_profile ALL;
foreach_profile = FOREACH gp_profile GENERATE COUNT($1);
dump foreach_profile;
```
(193)
```

### 在會員資料表中，年齡最大的會員為幾歲？
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
desc_age = ORDER userprofile BY $2 DESC;
limit_age = LIMIT desc_age 1;
foreach_age = FOREACH limit_age GENERATE $2;
dump foreach_age;

```
(75)
```

### 請問女性的會員數是多少？
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $1 == 'f';
gp_userprofile = GROUP filter_profile BY $1;
count_userprofile = FOREACH gp_userprofile GENERATE $0, COUNT($1);
dump count_userprofile;
```
(f,137)
```

### 在會員資料表中，年齡最小的會員為幾歲？
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
asc_age = ORDER userprofile BY $2 ASC;
limit_age = LIMIT asc_age 1;
foreach_age = FOREACH limit_age GENERATE $2;
dump foreach_age;
```
(3)
```

### 請依據資料集，查詢出會員數量排行，並顯示出人數第2多的國家為何？

> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
gp_country = GROUP userprofile BY $3;
count_coutry = FOREACH gp_country GENERATE $0, COUNT($1);
desc_country = ORDER count_coutry BY $1 DESC;
limit_country = LIMIT desc_country 2;
dump limit_country;
```
(Canada,60)
(Germany,35)

Ans: Germany
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
### 請依據資料集，查詢出熱門歌曲排行榜中，第7名歌曲名稱為何？
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
gp_traname = GROUP userdemand BY $3;
count_traname = FOREACH gp_traname GENERATE $0, COUNT($1);
desc_traname = ORDER count_traname BY $1 DESC;
limit_traname = LIMIT desc_traname 8;
dump limit_traname;
```
(Intro,169)
(?????,80)
(Love Lockdown,74)
(Say You Will,74)
(Welcome To Heartbreak (Feat. Kid Cudi),71)
(Paranoid (Feat. Mr. Hudson),68)
(Heartless,66)
(Bad News,65)

Ans:Bad News
```
### 請依據資料集，查詢出點播次數小於2的歌手有幾位？
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
gp_artname = GROUP userdemand BY $2;
count_artname = FOREACH gp_artname GENERATE $0, COUNT($1);
filter_artname = FILTER count_artname BY $1 < 2;
gp_userdemand = GROUP filter_artname ALL;
count_userdemand = FOREACH gp_userdemand GENERATE COUNT($1);
dump count_userdemand;
```
(8764)
```
## 999004 跟 999005 均會用到
### 國名B開頭的各國熱門歌曲第一名的名稱分別是什麼，請以國家名稱由A至Z排序？
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);

> filter_country = FILTER userprofile BY $3 matches 'B.*';
gp_country = GROUP filter_country BY $3;
count_traname = FOREACH gp_country GENERATE $1.$0,$0, COUNT($1);

> join1 = JOIN userdemand BY $0, userprofile BY $0;
foreach_join1 = FOREACH join1 GENERATE $3, $7;
filter_country = FILTER foreach_join1 BY $1 matches 'B.*';
gp_country = GROUP filter_country BY $1;
count_coutry = FOREACH gp_country GENERATE $0,COUNT($1);

```
(Brazil,8722)
(Belgium,2967)
(British Indian Ocean Territory,649)
(Bulgaria,364)
```
> filter_country = FILTER foreach_join1 BY $1 == 'Brazil';
gp_traname = GROUP filter_country BY $0;
count_traname = FOREACH gp_traname GENERATE $0, COUNT($1);
desc_traname = ORDER count_traname BY $1 DESC;
limit_traname = LIMIT desc_traname 2;
dump limit_traname;
```
(Intro,17)

Ans: (Brazil,Intro)
```
> filter_country = FILTER foreach_join1 BY $1 == 'Belgium';
gp_traname = GROUP filter_country BY $0;
count_traname = FOREACH gp_traname GENERATE $0, COUNT($1);
desc_traname = ORDER count_traname BY $1 DESC;
limit_traname = LIMIT desc_traname 2;
dump limit_traname;
```
(Propane Nightmares,22)

Ans: (Belgium, Propane Nightmares)
```

> filter_country = FILTER foreach_join1 BY $1 == 'British Indian Ocean Territory';
gp_traname = GROUP filter_country BY $0;
count_traname = FOREACH gp_traname GENERATE $0, COUNT($1);
desc_traname = ORDER count_traname BY $1 DESC;
limit_traname = LIMIT desc_traname 2;
dump limit_traname;
```
(Howl,6)

Ans: (British Indian Ocean Territory,Howl)
```

> filter_country = FILTER foreach_join1 BY $1 == 'Bulgaria';
gp_traname = GROUP filter_country BY $0;
count_traname = FOREACH gp_traname GENERATE $0, COUNT($1);
desc_traname = ORDER count_traname BY $1 DESC;
limit_traname = LIMIT desc_traname 2;
dump limit_traname;
```
(Swallowed,4)

Ans: (Bulgaria,Swallowed)
```




