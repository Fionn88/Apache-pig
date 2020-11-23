# 106模擬題
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

### (1)總註冊人數最多的五個國家？ (2)總註冊人數最少的國家?
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid:chararray, gender:chararray,age:int,country:chararray,registered:chararray);
gp_userorofile = GROUP userprofile BY $3;
count_userprofile = FOREACH gp_userorofile GENERATE $0, COUNT($1);
desc_userprofile = ORDER count_userprofile BY $1 DESC;
dump desc_userprofile;
```
(1)
(Canada,60)
(Germany,35)
(China,34)
(Taiwan,20)
(Poland,19)

(2)
(Armenia,1)
(British Indian Ocean Territory,1)
(Bulgaria,1)
(Canada Minor Outlying Islands,1)
(Estonia,1)
(Ireland,1)
(Japan,1)
(Latvia,1)
(Morocco,1)
(Nicaragua,1)
(Peru,1)
(Thailand,1)
(Venezuela,1)
```

### (1)註冊時間最早的三位使用者？(2)註冊時間最晚的三位使用者？
> (1)
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid:chararray, gender:chararray,age:int,country:chararray,registered:chararray);
foreach_profile = FOREACH userprofile GENERATE $0, STRSPLIT($4, '-', 3);
filter_profile = FILTER foreach_profile BY $1.$2 == 4;
dump filter_profile;

```
(user_000210,(12,Feb,04))
(user_000168,(18,Apr,04))
(user_000217,(2,Aug,04))
```
> (2)
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid:chararray, gender:chararray,age:int,country:chararray,registered:chararray);
foreach_profile = FOREACH userprofile GENERATE $0, STRSPLIT($4, '-', 3);
filter_profile = FILTER foreach_profile BY $1.$2 ==7;
dump filter_profile;
```
(user_000246,(2,Sep,07))
(user_000017,(27,Aug,07))
(user_000651,(31,Jul,07))
(user_000289,(31,Jul,07))
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
## 999004 跟 999005 均會用到
### (1)點播總次數最多的三位使用者？(2)點播總次數最少的三位使用者？
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
join1 = JOIN userdemand BY $0, userprofile BY $0;
foreach_join1 = FOREACH join1 GENERATE $0, $3;
gp_join1 = GROUP foreach_join1 BY $0;
foreach_join2 = FOREACH gp_join1 GENERATE $0,COUNT($1);
desc_join1 = ORDER foreach_join2 BY $1 DESC;
dump desc_join1;
```
(1)
(user_000233,3459)
(user_000349,3427)
(user_000033,2873)
(2)
(user_000282,6)
(user_000364,3)
(user_000248,1)
(user_000101,1)
(user_000301,1)
```

### (1)被點播總次數最多的歌手？ (2)被點播總次數最少的歌手？
> (1)
userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
join1 = JOIN userdemand BY $0, userprofile BY $0;
gp_join1 = GROUP join1 BY $2;
foreach_join1 = FOREACH gp_join1 GENERATE $0, COUNT($1);
desc_join1 = ORDER foreach_join1 BY $1 DESC;
limit_join1 = LIMIT desc_join1 5;
dump limit_join1;
```
(Radiohead,997)
```
> (2)
userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
join1 = JOIN userdemand BY $0, userprofile BY $0;
gp_join1 = GROUP join1 BY $2;
foreach_join1 = FOREACH gp_join1 GENERATE $0, COUNT($1);
asc_join1 = ORDER foreach_join1 BY $1 ASC;
limit_join1 = LIMIT asc_join1 5;
dump limit_join1;
```
("Bruno Coulais, The ChildrenS Choir Of Nice, Teri Hatcher, Bernard Paganotti, Hungrarian Symphony Orchestra Budapest & Laurent Petitgirard",1)
(3,1)
(O,1)
(P,1)
(12,1)
```

### (1)男性會員中，哪首歌曲被點播總次數最高？(2)女性會員中，哪首歌曲被點播總次數最高？
> (1)
userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
join1 = JOIN userdemand BY $0, userprofile BY $0;
foreach_join1 = FOREACH join1 GENERATE $0, $3, $5;
filter_join1 = FILTER foreach_join1 BY $2 == 'm';
gp_join1 = GROUP filter_join1 BY $1;
foreach_join2 = FOREACH gp_join1 GENERATE $0,COUNT($1);
desc_join1 = ORDER foreach_join2 BY $1 DESC;
limit_join1 = LIMIT desc_join1 5;
dump limit_join1;
```
(Intro,120)
```
> (2)
userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
join1 = JOIN userdemand BY $0, userprofile BY $0;
foreach_join1 = FOREACH join1 GENERATE $0, $3, $5;
filter_join1 = FILTER foreach_join1 BY $2 == 'f';
gp_join1 = GROUP filter_join1 BY $1;
foreach_join2 = FOREACH gp_join1 GENERATE $0,COUNT($1);
desc_join1 = ORDER foreach_join2 BY $1 DESC;
limit_join1 = LIMIT desc_join1 5;
dump limit_join1;
```
(?????,71)
```

### (1)18歲 ~ 24歲的會員中 (包括18歲與24歲)，哪首歌曲被點播總次數最高？ (2)25歲 ~ 34歲的會員中 (包括25歲與34歲)，哪首歌曲被點播總次數最高？
> (1)
userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $2 > 17 AND NOT $2 > 24;
join1 = JOIN userdemand BY $0, filter_profile BY $0;
gp_join1 = GROUP join1 BY $3;
count_join1 = FOREACH gp_join1 GENERATE $0, COUNT($1);
desc_join1 = ORDER count_join1 BY $1 DESC;
limit_join1 = LIMIT desc_join1 5;
dump limit_join1;
```
(Intro,97)
```

> (2)
userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $2 > 24 AND NOT $2 > 34;
join1 = JOIN userdemand BY $0, filter_profile BY $0;
gp_join1 = GROUP join1 BY $3;
count_join1 = FOREACH gp_join1 GENERATE $0, COUNT($1);
desc_join1 = ORDER count_join1 BY $1 DESC;
limit_join1 = LIMIT desc_join1 5;
dump limit_join1;

```
(Intro,58)
```

### (1)美國熱門歌曲排行前5名？(2)英國熱門歌曲排行前5名？
> (1)
userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $3 == 'United States';
join1 = JOIN userdemand BY $0, filter_profile BY $0;
gp_join1 = GROUP join1 BY $3;
count_join1 = FOREACH gp_join1 GENERATE $0, COUNT($1);
desc_join1 = ORDER count_join1 BY $1 DESC;
limit_join1 = LIMIT desc_join1 5;
dump limit_join1;
```
(Atlantis To Interzone,20)
("As Above, So Below",19)
(Golden Skans,17)
(GravityS Rainbow,17)
(Vengeance,16)
```
> (2)
userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $3 == 'United Kingdom';
join1 = JOIN userdemand BY $0, filter_profile BY $0;
gp_join1 = GROUP join1 BY $3;
count_join1 = FOREACH gp_join1 GENERATE $0, COUNT($1);
desc_join1 = ORDER count_join1 BY $1 DESC;
limit_join1 = LIMIT desc_join1 20;
dump limit_join1;
```
(Dex End Credit / Dtw End,5)
(Mopedgang,5)
(Me Gustas Tu,4)
(Das Lied Mit Den Suggestivfragen,4)
(La Parade,4)
```