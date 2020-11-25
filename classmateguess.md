# 猜猜題

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
### 20歲(包括)以上的男性有幾人?

> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $1 == 'm' AND $2 > 19;
gp_profile = GROUP filter_profile ALL;
count_profile = FOREACH gp_profile GENERATE COUNT($1);
dump count_profile;

```
(158)
```

### 加拿大女性有多少?

> serprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $1 == 'f' AND $3 == 'Canada';
gp_profile = GROUP filter_profile ALL;
count_profile = FOREACH gp_profile GENERATE COUNT($1);
dump count_profile;

```
(31)
```
### 年紀65歲以上有幾人?

> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $2 > 64;
gp_profile = GROUP filter_profile ALL;
count_profile = FOREACH gp_profile GENERATE COUNT($1);
dump count_profile;

```
(5)
```

### 總註冊人數最少的三個國家

> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
gp_userorofile = GROUP userprofile BY $3;
count_userprofile = FOREACH gp_userorofile GENERATE $0, COUNT($1);
asc_userprofile = ORDER count_userprofile BY $1 ASC;
dump asc_userprofile;

```
(Japan,1)
(Latvia,1)
(Armenia,1)
(Estonia,1)
(Peru,1)
(Ireland,1)
(Morocco,1)
(Bulgaria,1)
(Thailand,1)
(Nicaragua,1)
(Venezuela,1)
(Canada Minor Outlying Islands,1)
(Trinidad and Tobago,2)
(Serbia,2)
(Greece,2)
(New Zealand,2)
(Hungary,2)
(Czech Republic,2)
(Portugal,2)
(Slovakia,2)
(Croatia,3)
(Switzerland,3)
(Argentina,3)
(Romania,3)
(Chile,3)
(Belgium,3)
```

### 2005和2007美國的註冊人數統計?

> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
foreach_profile = FOREACH userprofile GENERATE $0,$3, STRSPLIT($4, '-', 3);
filter_profile = FILTER foreach_profile BY $1 == 'United States';
filter_profile2 = FILTER filter_profile BY $2.$2 == 5 OR $2.$2 == 7;
gp_profile = GROUP filter_profile2 ALL;
foreach_profile2 = FOREACH gp_profile GENERATE COUNT($1);
```
(6)
```

## 999004 跟 999005 均會用到
## 999005 - 使用者點聽紀錄
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
```
欄位名稱
使用者id  userid chararray
點聽時間  time chararray
歌手名稱  artname chararray
歌曲名稱  traname chararray
```

### 請問熱門歌曲男性聽眾，排行榜第一名到第十名它們的演唱者，歌手，點播次數為多少?
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
filter_profile = FILTER userprofile BY $1 == 'm';
join1 = JOIN filter_profile BY $0, userdemand BY $0;
gp_join = GROUP join1 BY ($7,$8);
count_join = FOREACH gp_join GENERATE $0,COUNT($1);
asc_join = ORDER count_join BY $1 ASC;
dump asc_join;
```
((Kanye West,Say You Will),74)
((Kanye West,Love Lockdown),71)
((Kanye West,Welcome To Heartbreak (Feat. Kid Cudi)),71)
((Kanye West,Paranoid (Feat. Mr. Hudson)),68)
((Kanye West,Coldest Winter),64)
((Kanye West,Bad News),62)
((Kanye West,Heartless),59)
((Kanye West,See You In My Nightmares),58)
((Kanye West,Amazing (Feat. Young Jeezy)),55)
((Kanye West,Pinocchio Story (Freestyle Live From Singapore)),55)
((Kanye West,Robocop),54)
```

### 請問註冊時間在2006年的女性使用者，點聽時間在2008年，的熱門歌曲為第一名，演唱者，歌名，點播次數為多少?
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
filter_profile = FILTER userprofile BY $1 == 'f' AND $4 matches '.*06';
filter_demand = FILTER userdemand BY $1 matches '2008.*';
join1 = JOIN filter_profile BY $0, filter_demand BY $0;
gp_join = GROUP join1 BY ($7,$8);
count_join = FOREACH gp_join GENERATE $0,COUNT($1);
asc_join = ORDER count_join BY $1 ASC;
dump asc_join;
```
((Jos? Gonz?lez,Crosses),8)
```

### 請問會員數量排行第七名的國家，和這個國家的總點播次數為多少?
- 所有國家點播數量
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
join1 = JOIN userdemand BY $0, userprofile BY $0;
gp_userprofile1 = GROUP join1 BY $7;
count_userprofile1 = FOREACH gp_userprofile1 GENERATE $0, COUNT($1);
dump count_userprofile1;

- 所有國家會員數量
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
(United States,9255)
```


### 請問會員年齡20歲以下、20-40歲、41-60歲、60歲以上各有多少人，各年齡層的熱門歌曲第一名,演唱者,歌名,點播次數為多少?

- 小於 20 歲 熱門歌曲第一名，演唱者，歌名，點播次數
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY NOT $2 > 20;
join1 = JOIN userdemand BY $0, filter_profile BY $0;
gp_join1 = GROUP join1 BY ($2,$3);
count_join1 = FOREACH gp_join1 GENERATE $0, COUNT($1);
desc_join1 = ORDER count_join1 BY $1 DESC;
limit_join1 = LIMIT desc_join1 5;
dump limit_join1;
```
((Britney Spears,Gimme More),32)
((植松伸夫,Somnus Memoria),32)
```
- 小於 20 會員數量
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY NOT $2 > 20;
gp_userprofile2 = GROUP filter_profile ALL;
count_userprofile2 = FOREACH gp_userprofile2 GENERATE $0, COUNT($1);
dump count_userprofile2;
```
(all,63)
```
- 20 - 40 歲 熱門歌曲第一名，演唱者，歌名，點播次數
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $2 > 19 AND NOT $2 > 40;
join1 = JOIN userdemand BY $0, filter_profile BY $0;
gp_join1 = GROUP join1 BY ($2,$3);
count_join1 = FOREACH gp_join1 GENERATE $0, COUNT($1);
desc_join1 = ORDER count_join1 BY $1 DESC;
limit_join1 = LIMIT desc_join1 5;
dump limit_join1;
```
((Kanye West,Say You Will),72)
```
- 20 - 40 會員數量
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $2 > 19 AND NOT $2 > 40;
gp_userprofile2 = GROUP filter_profile ALL;
count_userprofile2 = FOREACH gp_userprofile2 GENERATE $0, COUNT($1);
```
(all,260)
```

- 41 - 60 歲 熱門歌曲第一名，演唱者，歌名，點播次數
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $2 > 40 AND NOT $2 > 60;
join1 = JOIN userdemand BY $0, filter_profile BY $0;
gp_join1 = GROUP join1 BY ($2,$3);
count_join1 = FOREACH gp_join1 GENERATE $0, COUNT($1);
desc_join1 = ORDER count_join1 BY $1 DESC;
limit_join1 = LIMIT desc_join1 5;
dump limit_join1;
```
((Emmy The Great,My Party Is Better Than Yours (Demo)),3)
```

- 41 - 60 會員數量
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $2 > 40 AND NOT $2 > 60;
gp_userprofile2 = GROUP filter_profile ALL;
count_userprofile2 = FOREACH gp_userprofile2 GENERATE $0, COUNT($1);
```
(all,9)
```
- 60以上 歲 熱門歌曲第一名，演唱者，歌名，點播次數
> userdemand = LOAD '/dataset/999005/999005.tsv' USING PigStorage('\t') AS (userid: chararray, time:chararray, artname: chararray, traname:chararray);
userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $2 > 59;
join1 = JOIN userdemand BY $0, filter_profile BY $0;
gp_join1 = GROUP join1 BY ($2,$3);
count_join1 = FOREACH gp_join1 GENERATE $0, COUNT($1);
desc_join1 = ORDER count_join1 BY $1 DESC;
limit_join1 = LIMIT desc_join1 5;
dump limit_join1;
```
((Jens Lekman,A Postcard To Nina),3)
```
- 60以上 會員數量
> userprofile = LOAD '/dataset/999004/999004.tsv' USING PigStorage('\t') AS (userid: chararray, gender:chararray, age: int, country:chararray, registered: chararray);
filter_profile = FILTER userprofile BY $2 > 59;
gp_userprofile2 = GROUP filter_profile ALL;
count_userprofile2 = FOREACH gp_userprofile2 GENERATE $0, COUNT($1);
```
(all,6)
```
## 5958 - 各縣(市)警察(分)局暨所屬分駐(派出)所地址資料
> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);

```
 欄位名稱
名稱       name:chararray
郵遞區號   zip_code:chararray
地址       address:chararray

原始資料集內容
     name    zip_code    address
臺北市政府警察局,100,臺北市中正區延平南路96號
中山分局,104,臺北市中山區中山北路2段1號
中山一派出所,104,臺北市中山區中山北路1段110號
```

### 請問擁有最多警察局的都市是哪個?
> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);
foreach_police = FOREACH police GENERATE $0,SUBSTRING($2,0,3);
gp_police = GROUP foreach_police BY $1;
count_police = FOREACH gp_police GENERATE $0,COUNT($1);
desc_police = ORDER count_police BY $1 DESC;
limit_police = LIMIT desc_police 1;
dump limit_police; 
```
(新北市,176)
```

### 臺北市大安區除了派出所的警察單位的名字與地址?
> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);
filter_police = FILTER police BY $2 matches '臺北市大安區.*';
foreach_police = FOREACH filter_police GENERATE $0,$2;
```
(大安分局,臺北市大安區仁愛路3段2號)
```

## 24333 –「ATM位置」查詢一覽表
> atm = LOAD '/dataset/24333/24333.csv' USING PigStorage(',') AS (code: chararray, name: chararray, location: chararray, city: chararray, address:chararray);
```
欄位名稱
裝設金融機構代號  code:chararray
裝設金融機構名稱  name:chararray
裝設地點  location:chararray
裝設縣市  city:chararray
裝設地址  address:chararray

原始資料集內容
code name  location city               address
004,臺灣銀行,士林分行,台北市,台北市士林區中山北路六段197號
004,臺灣銀行,大同公司,台北市,台北市中山區中山北路三段22號
004,臺灣銀行,大安分行,台北市,台北市大安區敦化南路二段69號1樓
```
## 24333 跟 5989 均會用到
### 請問最多警察局的都市他們的ATM總共為幾台?
- 先算出最多警察局的都市
> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);
foreach_police = FOREACH police GENERATE $0,SUBSTRING($2,0,3);
gp_police = GROUP foreach_police BY $1;
count_police = FOREACH gp_police GENERATE $0,COUNT($1);
desc_police = ORDER count_police BY $1 DESC;
limit_police = LIMIT desc_police 1;
dump limit_police; 
```
(新北市,176)
```
- 再用最多都市的警察局過濾
> atm = LOAD '/dataset/24333/24333.csv' USING PigStorage(',') AS (code: chararray, name: chararray, location: chararray, city: chararray, address:chararray);
filter_atm = FILTER atm BY $3 == '新北市';
gp_atm = GROUP filter_atm BY $3;
count_atm = FOREACH gp_atm GENERATE $0,COUNT($1);
dump count_atm;
```
(新北市,3774)
```

### 請問最多警察局的都市，平均一間警察局要管理多少ATM(求到小數點後第二位，四捨五入)?
- 先算出最多警察局的都市
> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);
foreach_police = FOREACH police GENERATE $0,SUBSTRING($2,0,3);
gp_police = GROUP foreach_police BY $1;
count_police = FOREACH gp_police GENERATE $0,COUNT($1);
desc_police = ORDER count_police BY $1 DESC;
limit_police = LIMIT desc_police 1;
dump limit_police; 
```
(新北市,176)
```
- 再用最多都市的警察局過濾
> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);
foreach_police = FOREACH police GENERATE $0,SUBSTRING($2,0,3);
filter_police = FILTER foreach_police BY $1 == '新北市';
gp_police = GROUP foreach_police BY $1;
count_police = FOREACH gp_police GENERATE $0,COUNT($1);

>atm = LOAD '/dataset/24333/24333.csv' USING PigStorage(',') AS (code: chararray, name: chararray, location: chararray, city: chararray, address:chararray);
filter_atm = FILTER atm BY $3 == '新北市';
gp_atm = GROUP filter_atm BY $3;
count_atm = FOREACH gp_atm GENERATE $0,COUNT($1);
join1 = JOIN count_atm BY $0,count_police BY $0;
foreach_join1 = FOREACH join1 GENERATE $0,ROUND_TO($1/$3,2);
dump foreach_join1;
```
(新北市,21.0)
```
