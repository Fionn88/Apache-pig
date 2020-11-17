# 猜題大哥大

## 20445 - 替代役役男訓練人數統計表

```
欄位名稱
年度   year:int
梯次   phase:chararray
替代役役男訓練人數   trainees:int

原始資料集內容
year phase trainees
100,91,1079
100,92,969
100,92_2,122
```

> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);

### 93年度到106年度，哪一年的替代役男訓練人數最多 ?

>  soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 > 92) AND (NOT $0 > 106);
gp_foreach_filter_soldier = GROUP filter_soldier BY $0;
sum_gp_filter_soldier = FOREACH gp_foreach_filter_soldier GENERATE $0,SUM($1.$2);
order_sum_gp_filter_soldier = ORDER sum_gp_filter_soldier BY $1 DESC;
limit_filter_soldier = LIMIT order_sum_gp_filter_soldier 1;
```
(103,37210)
```
### 哪一年的梯次最多?
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
gp_soldier = GROUP soldier BY $0;
foreach_soldier = FOREACH gp_soldier GENERATE $0,COUNT($1);
desc_soldier = ORDER foreach_soldier BY $1 DESC;
limit_soldier = LIMIT desc_soldier 1;
dump limit_soldier;

### 找出99年度所有資料
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY $0 == 99;
dump filter_soldier;
```
(99,79,734)
(99,80,900)
(99,80_2,112)
(99,81,1310)
(99,82,1057)
(99,83,866)
(99,84,2577)
(99,84_2,157)
(99,85,2521)
(99,86,2581)
(99,87,2443)
(99,87_2,195)
(99,88,2439)
(99,89,2376)
(99,90,1281)
(99,90_2,164)
```

### 找出99年度86梯次所有資料
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier2 = FILTER filter_soldier BY $1 == '86';
dump filter_soldier2;
```
(99,86,2581)
```

### 找出人數前三名
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
desc_soldier = ORDER soldier BY $2 DESC;
limit_desc_soldier = LIMIT desc_soldier 3;
dump limit_desc_soldier; 

```
(103,142,3853)
(103,143,3701)
(104,156,3639)
```
### 找出服役人數最多的年份
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
gp_soldier = GROUP soldier BY $0;
sum_soldier = FOREACH gp_soldier GENERATE $0, SUM($1.$0);
desc_sum_soldier = ORDER sum_soldier BY $1 DESC;
limit_ desc_sum_soldier = LIMIT desc_sum_soldier 1;

```
(104,2392)
```

### 99及98年的訓練人數加總
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 == 99) OR ($0 == 98);
foreach_filter_soldier = FOREACH filter_soldier GENERATE $0,$2;
gp_foreach_filter_soldier = GROUP foreach_filter_soldier all;
sum_ gp_filter_soldier = FOREACH gp_foreach_filter_soldier GENERATE SUM($1.$1);
dump sum_gp_filter_soldier;

```
46039
```

### 93年度到106年度，共徵招了多少梯次的替代役男 ?
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 > 92) AND (NOT $0 > 107);
gp_foreach_filter_soldier = GROUP filter_soldier all;
count_gp_filter_soldier = FOREACH gp_foreach_filter_soldier GENERATE COUNT($1);
dump count_gp_filter_soldier;

```
200
```

### 93年度到106年度，替代役役男訓練人數最少的前三個梯次?
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 > 92) AND (NOT $0 > 107);
order_filter_soldier = ORDER filter_soldier BY $2 ASC;
limit_order_filter_soldier = LIMIT order_filter_soldier 3;
dump limit_order_filter_soldier;

```
(106,184_2,60)
(96,49_2,61)
(106,178_2,61)
```

### 93年度到106年度，共有多少位替代役役男參加訓練 ?
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 > 92) AND (NOT $0 > 106);
foreach_filter_soldier = FOREACH filter_soldier GENERATE $0,$2;
gp_foreach_filter_soldier = GROUP foreach_filter_soldier all;
sum_gp_filter_soldier = FOREACH gp_foreach_filter_soldier GENERATE SUM($1.$1);
dump sum_gp_filter_soldier;

```
312017
```

### 93年度到105年度，共徵招了幾個梯次的替代役役男 ?
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 > 92) AND (NOT $0 > 105);
gp_foreach_filter_soldier = GROUP filter_soldier all;
count_gp_filter_soldier = FOREACH gp_foreach_filter_soldier GENERATE COUNT($1);
dump count_gp_filter_soldier;

```
183
```

### 94年度到105年度，共有多少位替代役役男參加訓練 ?
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 > 93) AND (NOT $0 > 105);
foreach_filter_soldier = FOREACH filter_soldier GENERATE $0,$2;
gp_foreach_filter_soldier = GROUP foreach_filter_soldier all;
sum_gp_filter_soldier = FOREACH gp_foreach_filter_soldier GENERATE SUM($1.$1);
dump sum_gp_filter_soldier;

```
268669
```

### 100年度，共徵招了幾個梯次的替代役役男 ?
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 == 100);
gp_foreach_filter_soldier = GROUP filter_soldier all;
count_gp_filter_soldier = FOREACH gp_foreach_filter_soldier GENERATE COUNT($1);
dump count_gp_filter_soldier;

```
16
```

### 100年度到103年度，共徵招了幾個梯次的替代役役男 ?
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 > 99) AND (NOT $0 > 103);
gp_foreach_filter_soldier = GROUP filter_soldier all;
count_gp_filter_soldier = FOREACH gp_foreach_filter_soldier GENERATE COUNT($1);
dump count_gp_filter_soldier;

```
71
```

### 93年度，每一梯次平均招募的替代役役男訓練人數是多少 ?
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 == 93);
gp_filter_soldier = GROUP filter_soldier BY $1;
avg_gp_filter_soldier = FOREACH gp_filter_soldier GENERATE $0, AVG($1.$2);
dump avg_gp_filter_soldier;

```
(23, 1914.0)
(24,1942.0)
(25, 1877.0)
(26, 1468.0)
(27, 1780.0)
(28, 1903.0)
(29, 1965.0)
(30, 1947.0)
```

### 93年度到106年度，哪一年的每一梯次平均招募的替代役役男訓練人數最少 ?
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 > 92) AND (NOT $0 > 106);
gp_filter_soldier = GROUP filter_soldier BY $0;
avg_gp_filter_soldier = FOREACH gp_filter_soldier GENERATE $0, AVG($1.$2);
order_avg_gp_filter_soldier = ORDER avg_gp_filter_soldier BY $1 ASC;
dump order_avg_gp_filter_soldier;

```
(104,1318.0434782608695)
```

### 93年度到106年度，每一梯次平均共招募多少人 ?
> soldier = LOAD '/dataset/20445/20445.csv' USING PigStorage(',') AS(year:int,echelon:chararray,people:int);
filter_soldier = FILTER soldier BY ($0 > 92) AND (NOT $0 > 106);
gp_filter_soldier = GROUP filter_soldier BY $1;
avg_gp_filter_soldier = FOREACH gp_filter_soldier GENERATE $0, AVG($1.$2);
dump avg_gp_filter_soldier;
```
(23,1914.0)
(24,1942.0)
(25,1877.0)
(26,1468.0)
(27,1780.0)
(28,1903.0)
(29,1965.0)
(30,1947.0)
(31,1775.0)
(32,2023.0)
(33,1904.0)
(34,1603.0)
(35,1771.0)
(36,2017.0)
(37,2095.0)
(38,2067.0)
(39,2040.0)
(40,1980.0)
(41,2030.0)
(42,1672.0)
(43,1540.0)
(44,2061.0)
(45,2053.0)
(46,2076.0)
(47,2073.0)
(48,2046.0)
(49,1884.0)
(50,1861.0)
(51,2054.0)
(52,2173.0)
(53,2223.0)
(54,2070.0)
(55,2234.0)
(56,2205.0)
(57,1883.0)
(58,1608.0)
(59,1668.0)
(60,1638.0)
(61,2224.0)
(62,2130.0)
(63,2337.0)
(64,2374.0)
(65,2343.0)
(66,2356.0)
(67,2412.0)
(68,2325.0)
(69,1654.0)
(70,1374.0)
(71,858.0)
(72,2598.0)
(73,2608.0)
(74,2386.0)
(75,2157.0)
(76,2238.0)
(77,1976.0)
(78,1109.0)
(79,734.0)
(80,900.0)
(81,1310.0)
(82,1057.0)
(83,866.0)
(84,2577.0)
(85,2521.0)
(86,2581.0)
(87,2443.0)
(88,2439.0)
(89,2376.0)
(90,1281.0)
(91,1079.0)
(92,969.0)
(93,1102.0)
(94,895.0)
(95,910.0)
(96,1713.0)
(97,981.0)
(98,2680.0)
(99,2716.0)
(100,2645.0)
(101,2600.0)
(102,2489.0)
(103,1212.0)
(104,1097.0)
(105,1076.0)
(106,1049.0)
(107,1184.0)
(108,945.0)
(109,1358.0)
(110,2601.0)
(111,2874.0)
(112,2901.0)
(113,2870.0)
(114,2418.0)
(115,2045.0)
(116,1330.0)
(117,1187.0)
(118,1756.0)
(119,1870.0)
(120,833.0)
(121,2816.0)
(122,2933.0)
(123,3479.0)
(124,3501.0)
(125,3545.0)
(126,3461.0)
(127,2846.0)
(128,2974.0)
(129,2876.0)
(130,1480.0)
(131,1409.0)
(132,1056.0)
(133,2014.0)
(134,943.0)
(135,1809.0)
(136,1547.0)
(137,2897.0)
(138,2820.0)
(139,3167.0)
(140,2954.0)
(141,3542.0)
(142,3853.0)
(143,3701.0)
(144,3114.0)
(145,1561.0)
(146,1291.0)
(147,757.0)
(148,768.0)
(149,917.0)
(150,930.0)
(151,1750.0)
(152,1368.0)
(153,2354.0)
(154,3083.0)
(155,3041.0)
(156,3639.0)
(157,3227.0)
(158,1961.0)
(159,1306.0)
(160,1455.0)
(174,2242.0)
(175,1891.0)
(176,1541.0)
(177,1050.0)
(178,2664.0)
(179,2587.0)
(180,2734.0)
(181,2569.0)
(182,2768.0)
(183,2887.0)
(184,2601.0)
(185,1812.0)
(186,845.0)
(35_2,108.0)
(37_2,103.0)
(43_2,119.0)
(45_2,126.0)
(47_2,66.0)
(49_2,61.0)
(51_2,116.0)
(53_2,175.0)
(55_2,109.0)
(58_2,112.0)
(61_2,131.0)
(63_2,173.0)
(65_2,97.0)
(68_2,124.0)
(72_2,157.0)
(75_2,183.0)
(77_2,167.0)
(80_2,112.0)
(84_2,157.0)
(87_2,195.0)
(90_2,164.0)
(92_2,122.0)
(96_2,108.0)
(101_2,140.0)
(103_2,98.0)
(105_2,90.0)
(109_2,153.0)
(112_2,193.0)
(115_2,97.0)
(117_2,82.0)
(119_2,66.0)
(121_2,161.0)
(125_2,171.0)
(128_2,221.0)
(131_2,112.0)
(136_2,155.0)
(140_2,298.0)
(143_2,339.0)
(147_2,148.0)
(152_2,127.0)
(153_2,101.0)
(155_2,148.0)
(156_2,106.0)
(158_2,163.0)
(159_2,114.0)
(174-2,138.0)
(178_2,61.0)
(181_2,102.0)
(184_2,60.0)
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

### 最多派出所的郵遞區號是幾號？
> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);
filter_police = FILTER police BY $0 matches '.*派出所';
gp_police = GROUP filter_police BY $1;
foreach_police = FOREACH gp_police GENERATE $0,COUNT($1);
desc_police = ORDER foreach_police BY $1 DESC;
limit_police = LIMIT desc_police 1;
dump limit_police;
```
(546,21)
```

### 哪個縣市有最多派出所？
> police = LOAD '/dataset/5958/5958.csv' USING PigStorage(',') AS (name: chararray, code: chararray, address: chararray);
filter_police = FILTER police BY $0 matches '.*派出所';
foreach_police = FOREACH filter_police GENERATE $0,SUBSTRING($2,0,3);
gp_police = GROUP foreach_police BY $1;
count_police = FOREACH gp_police GENERATE $0,COUNT($1);
desc_police = ORDER count_police BY $1 DESC;
limit_police = LIMIT desc_police 1;
```
(新北市,145)
```

## 6086 - 107年幼兒園名錄
> kid = LOAD '/dataset/6086/6086.csv' Using PigStorage (',')  AS(code:chararray,school:chararray,city:chararray,address:chararray, phone:chararray);
```
欄位名稱
代碼 code:chararray
學校名稱 school:chararray
縣市名稱 city:chararray
地址 address:chararray
電話 phone:chararray

原始資料集內容
 code             school             city                  address           phone
011K02,新北市私立溫特爾幼兒園,新北市,新北市三峽區龍埔里5鄰三樹路336號1、2、3樓,(02)26718181
011K03,新北市私立新榮富新莊幼兒園,新北市,新北市新莊區中信里13鄰中和街204巷1、3號，218巷2、6號，中信里12鄰中和街1、3、5、7、11號,(02)29922174
011K04,新北市私立崇儒幼兒園,新北市,新北市中和區安樂里16鄰宜安路56之1號1樓,(02)29435789
```

### 幼兒園數量最少的是哪個縣市?
> kid = LOAD '/dataset/6086/6086.csv' Using PigStorage (',')  AS(code:chararray,school:chararray,city:chararray,address:chararray, phone:chararray);
gp_kid = GROUP kid BY $2;
foreach_kid = FOREACH gp_kid GENERATE $0,COUNT($1);
asc_kid = ORDER foreach_kid BY $1 ASC;
limit_kid = LIMIT asc_kid 1;
dump limit_kid;
```
(連江縣,5)
```

### 臺北市與新北市的幼兒園各有多少間? 由數量多到少排序。
> kid = LOAD '/dataset/6086/6086.csv' Using PigStorage (',')  AS(code:chararray,school:chararray,city:chararray,address:chararray, phone:chararray);
filter_kid = FILTER kid BY $2 == '臺北市' OR $2 == '新北市';
gp_kid = GROUP filter_kid BY $2;
foreach_kid = FOREACH gp_kid GENERATE $0,COUNT($1);
desc_kid = ORDER foreach_kid BY $1 DESC;
dump desc_kid;
```
(新北市,1134)
(臺北市,689)
```

## 6087 - 107年國民小學名錄
> element = LOAD '/dataset/6087/6087.csv' Using PigStorage (',')  AS(code:chararray,school:chararray,city:chararray,address:chararray, phone:chararray,url:chararray);
```
欄位名稱
代碼 code:chararray
學校名稱 school:chararray
縣市名稱 city:chararray
地址 address:chararray
電話 phone:chararray
網址 url:chararray

原始資料集內容
 code   school      city         address               phone            url
011601,私立育才國小,新北市,新北市永和區福和路125巷20號,(02)29214630,http://www.ytes.ntpc.edu.tw
011602,私立聖心國小,新北市,新北市八里區龍米路一段261號,(02)26182330,http://lshes.com/school/
011603,私立及人國小,新北市,新北市永和區文化路172號,(02)29212145,http://www.cjps.ntpc.edu.tw

```
### 新北市有多少間私立國小？
> element = LOAD '/dataset/6087/6087.csv' Using PigStorage (',')  AS(code:chararray,school:chararray,city:chararray,address:chararray, phone:chararray,url:chararray);
filter_element = FILTER element BY $2 == '新北市' AND SUBSTRING($1,0,2) == '私立';
gp_element = GROUP filter_element BY $2;
count_element = FOREACH gp_element GENERATE $0, COUNT($1);
dump count_element;
```
(新北市,5)
```

## 999003 - 107年6月行政區分齡兒童及少年性別人口統計_縣市
> teens = LOAD '/dataset/999003/999003.csv' USING PigStorage(',') AS (country_id: int, country: chararray, a0a5_cnt: int, a6a11_cnt:int, a12a17_cnt:int);
```
欄位名稱
縣市代碼  country_id:int
縣市名稱  country:chararray
0-5歲兒童人口數  a0a5_cnt:int
6-11歲兒童人口數  a6a11_cnt:int
12-17歲少年人口數  a12a17_cnt:int

原始資料集內容
country_id country a0a5_cnt a6a11_cnt a12a17_cnt
10002,宜蘭縣,20907,21718,27474
10015,花蓮縣,15380,15338,19695
09020,金門縣,6373,4437,5451
```

### 新北市的0~17歲兒童總數有多少個?
> teens = LOAD '/dataset/999003/999003.csv' USING PigStorage(',') AS (country_id: int, country: chararray, a0a5_cnt: int, a6a11_cnt:int, a12a17_cnt:int);
filter_teens = FILTER teens BY $1 == '新北市';
foreach_teens = FOREACH filter_teens GENERATE $1,$2+$3+$4; 
dump foreach_teens;
```
(新北市,620357)
```

## 12197_A1 -- A1類交通事故資料
> accident = LOAD '/dataset/12197_A1/12197_A1.csv' USING PigStorage(',') AS (time: chararray, dead: chararray, injured: chararray, vehicle: chararray);
```
欄位名稱
發生時間 time:chararray
死亡人數 dead:chararray
受傷人數 injured:chararray
車種 vehicle:chararray

原始資料集
          ctime           dead injured  vehicle
106年01月01日 02時35分00秒,死亡1,受傷0,普通重型-機車
106年01月01日 02時43分00秒,死亡1,受傷0,普通重型-機車
106年01月01日 03時35分00秒,死亡2,受傷0,普通重型-機車
```

### 造成事故最多的車種是哪種車? (造成死亡或受傷皆算事故)
> accident = LOAD '/dataset/12197_A1/12197_A1.csv' USING PigStorage(',') AS (time: chararray, dead: chararray, injured: chararray, vehicle: chararray);
gp_accident = GROUP accident BY $3;
count_accident = FOREACH gp_accident GENERATE $0,COUNT($1);
desc_accident = ORDER count_accident BY $1 DESC;
limit_accident = LIMIT desc_accident 1;
dump limit_accident;
```
(普通重型-機車,513)
```

### 發生事故最多的是哪年哪月哪日? (造成死亡或受傷皆算事故)
> accident = LOAD '/dataset/12197_A1/12197_A1.csv' USING PigStorage(',') AS (time: chararray, dead: chararray, injured: chararray, vehicle: chararray);
foreach_accident = FOREACH accident GENERATE SUBSTRING($0,0,10),$1,$2,$3;
gp_accident = GROUP foreach_accident BY $0;
count_accident = FOREACH gp_accident GENERATE $0,COUNT($1);
desc_accident = ORDER count_accident BY $1 DESC;
limit_accident = LIMIT desc_accident 1;
dump limit_accident;
```
(106年08月13日,10)
```

### 造成死亡總數最高的是哪個車種?
> accident = LOAD '/dataset/12197_A1/12197_A1.csv' USING PigStorage(',') AS (time: chararray, dead: chararray, injured: chararray, vehicle: chararray);
foreach_accident = FOREACH accident GENERATE SUBSTRING($1,2,3) AS dead:int ,$3;
gp_accident = GROUP foreach_accident BY $1;
sum_accident = FOREACH gp_accident GENERATE $0,SUM($1.$0);
desc_accident = ORDER sum_accident BY $1 DESC;
limit_accident = LIMIT desc_accident 1;
dump limit_accident;
```
(普通重型-機車,517)
```

## 12197_A2 – A2類交通事故資料
> accident2 = LOAD '/dataset/12197_A2/12197_A2.csv' USING PigStorage(',') AS (time: chararray, dead: chararray, injured: chararray, vehicle: chararray);
```
欄位名稱
發生時間 time:chararray
死亡人數 dead:chararray
受傷人數 injured:chararray
車種 vehicle:chararray

原始資料集內
ctime                    dead  injured    vehicle
106年01月01日 00時00分00秒,死亡0,受傷1,自用-小客車
106年01月01日 00時00分00秒,死亡0,受傷2,自用-小客車
106年01月01日 00時03分00秒,死亡0,受傷1,自用-小客車
```

### 平均造成受傷數最高的是哪個車種? (造成受傷人數總數/事故總數)，平均一樣時依車種字母大到小排序。
> accident2 = LOAD '/dataset/12197_A2/12197_A2.csv' USING PigStorage(',') AS (time: chararray, dead: chararray, injured: chararray, vehicle: chararray);
foreach_accident2 = FOREACH accident2 GENERATE SUBSTRING($2,2,3) AS injured:int, $3;
gp_accident2= GROUP foreach_accident2 BY $1;
avg_accident2 = FOREACH gp_accident2 GENERATE $0,AVG($1.$0);
desc_accident2 = ORDER avg_accident2 BY $1 DESC;
dump desc_accident2; 

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
### 哪間銀行的ATM在台中市有最多台?
> atm = LOAD '/dataset/24333/24333.csv' USING PigStorage(',') AS (code: chararray, name: chararray, location: chararray, city: chararray, address:chararray);
filter_atm = FILTER atm BY $3 == '台中市';
gp_atm = GROUP filter_atm BY $1;
count_atm = FOREACH gp_atm GENERATE $0,COUNT($1);
desc_atm = ORDER count_atm BY $1 DESC;
limit_atm = LIMIT desc_atm 1;
dump limit_atm;
```
(中國信託商業銀行,642)
```

### 哪個縣市擁有最多"臺灣銀行"的ATM?
> atm = LOAD '/dataset/24333/24333.csv' USING PigStorage(',') AS (code: chararray, name: chararray, location: chararray, city: chararray, address:chararray);
filter_atm = FILTER atm BY $1 == '台灣銀行' OR $1 == '臺灣銀行';
gp_atm = GROUP filter_atm BY $3;
count_atm = FOREACH gp_atm GENERATE $0,COUNT($1);
desc_atm = ORDER count_atm BY $1 DESC;
limit_atm = LIMIT desc_atm 1;
dump limit_atm;
```
(台北市,95)
```

## 8066 - 農產品交易行情
> farm = LOAD '/dataset/8066/8066.csv' USING PigStorage(',') AS (date: chararray, crop_code: chararray, crop_name: chararray, market_code: chararray, market_name:chararray, upper_price:float, middle_price:float, lower_price:float, average_price:float, trading_volume:int);
```
欄位名稱
交易日期  date:chararray
作物代號  crop_code:chararray
作物名稱  crop_name:chararray
市場代號  market_code:chararray
市場名稱  market_name:chararray
上價  upper_price:float
中價  middle_price:float
下價  lower_price:float
平均價  average_price:float
交易量  trading_volume:int

原始資料集內容
cdata crop_code crop_name market_code market_name upper_price middle_price lower_price average_price trading_volume
107.09.11,11,椰子,104,台北二,31,20,15.7,21.3,849
107.09.11,129,椰子-進口剝殼,104,台北二,88.3,72.8,60,73.3,60
107.09.11,31,釋迦,104,台北二,114,73.5,46.8,76.3,3581
```
### 全台農產品交易量最高的是哪個市場?
> farm = LOAD '/dataset/8066/8066.csv' USING PigStorage(',') AS (date: chararray, crop_code: chararray, crop_name: chararray, market_code: chararray, market_name:chararray, upper_price:float, middle_price:float, lower_price:float, average_price:float, trading_volume:int);
gp_farm = GROUP farm BY $4 ;
count_farm = FOREACH gp_farm GENERATE $0, SUM($1.$9);
desc_farm = ORDER count_farm BY $1 DESC;
limit_farm = LIMIT desc_farm 1;
dump limit_farm;
```
(台北一,1676906)
```

### 全台交易總量最高的是哪種農產品? ("百香果-其他"與"百香果-改良種"皆算是"百香果"，以此類推其他農產品名稱)

> farm = LOAD '/dataset/8066/8066.csv' USING PigStorage(',') AS (date: chararray, crop_code: chararray, crop_name: chararray, market_code: chararray, market_name:chararray, upper_price:float, middle_price:float, lower_price:float, average_price:float, trading_volume:int);
foreach_farm = FOREACH farm GENERATE STRSPLIT($2,'-',2),$9;
gp_farm = GROUP foreach_farm BY $0.$0;
sum_farm = FOREACH gp_farm GENERATE $0,SUM($1.$1);
desc_farm = ORDER sum_farm BY $1 DESC;
limit_farm = LIMIT desc_farm 1;
dump limit_farm;
```
(文旦柚,589354)
```
### 平均上價與平均下價平均價差最高的是哪項農產品? ("百香果-其他"與"百香果-改良種"算兩項不同的農產品，以此類推其他農產品名稱)

> farm = LOAD '/dataset/8066/8066.csv' USING PigStorage(',') AS (date: chararray, crop_code: chararray, crop_name: chararray, market_code: chararray, market_name:chararray, upper_price:float, middle_price:float, lower_price:float, average_price:float, trading_volume:int);
foreach_farm = FOREACH farm GENERATE $2,$5,$7;
gp_farm = GROUP foreach_farm BY $0;
avg_farm = FOREACH gp_farm GENERATE $0, AVG($1.$1), AVG($1.$2);
round_farm = FOREACH avg_farm GENERATE $0, ROUND_TO($1, 2),ROUND_TO($2, 2);
finish_farm = FOREACH round_farm GENERATE $0, $1-$2;
desc_farm = ORDER finish_farm BY $1 DESC;
limit_farm = LIMIT desc_farm 1;
dump limit_farm;

```
(葡萄-進口,334.6)
```

## 63029 - 十六縣持卡人前十大國外消費金額及筆數(依簽帳筆數排名)

> card = LOAD '/dataset/63029/63029.csv' USING PigStorage(',') AS (yaer_month: chararray, country: chararray, tw_city: chararray, amt:int, count:int);
```
欄位名稱
年月  year_month:chararray
國別  country:chararray
城市  tw_city:chararray
金額  amt:int
筆數  count:int

原始資料集內容
year_month country tw_city amt count
2014-01,英國,基隆市,20933333,30063
2014-01,盧森堡,基隆市,2575891,5276
2014-01,日本,基隆市,20238233,3895
```

### 2016到2018年國外消費總金額最高的是哪個縣市?

> card = LOAD '/dataset/63029/63029.csv' USING PigStorage(',') AS (yaer_month: chararray, country: chararray, tw_city: chararray, amt:int, count:int);
foreach_card = FOREACH card GENERATE SUBSTRING($0,0,4) AS year:int,$2, $3;
filter_card = FILTER foreach_card BY ($0 > 2015) AND (NOT $0 > 2018);
gp_card = GROUP filter_card BY $1;
sum_card = FOREACH gp_card GENERATE $0,SUM($1.$2);
desc_card = ORDER sum_card BY $1 DESC;
limit_card = LIMIT desc_card 1;

```
(新竹市,10005781918)
```
### 哪一個月的國外消費平均金額最高?

> card = LOAD '/dataset/63029/63029.csv' USING PigStorage(',') AS (yaer_month: chararray, country: chararray, tw_city: chararray, amt:int, count:int);
foreach_card = FOREACH card GENERATE SUBSTRING($0,5,7) ,$2, $3;
gp_card = GROUP foreach_card BY $0;
sum_card = FOREACH gp_card GENERATE $0,AVG($1.$2); 
foreach_card2 = FOREACH sum_card GENERATE $0,(int)$1;
desc_card = ORDER foreach_card2 BY $1 DESC;
limit_card = LIMIT desc_card 1;
replace_card = FOREACH limit_card GENERATE REPLACE($0,'06','六月'),$1;
dump replace_card;
```
(六月,11158768)
```

### 新竹市2018年在哪個國家的總消費金額最高?
> card = LOAD '/dataset/63029/63029.csv' USING PigStorage(',') AS (yaer_month: chararray, country: chararray, tw_city: chararray, amt:int, count:int);
filter_card = FILTER card BY $2 == '新竹市';
foreach_card  = FOREACH filter_card GENERATE SUBSTRING($0,0,4) AS year:int, $1,$3;
filter_card2 = FILTER foreach_card BY $0 == 2018;
gp_card = GROUP filter_card2 BY $1;
sum_card = FOREACH gp_card GENERATE $0, SUM($1.$2);
desc_card = ORDER sum_card BY $1 DESC;
limit_card = LIMIT desc_card 1;
dump limit_card;
```
(日本,548333518)
```

## 38315 -- 十六縣居民跨縣市消費樣態
> pay = LOAD '/dataset/38315/38315.csv' USING PigStorage(',') AS (yaer: chararray,area:chararray,type:chararray,cards:chararray,total_trans:int,total_amt:biginteger, inter_city_trans:int, inter_city_amt:biginteger);
```
欄位名稱
年月 year:chararray
地區 area:chararray
類別 type:chararray
卡數 cards:int
總交易筆數 total_trans:int
總交易金額[新台幣] total_amt:biginteger
跨縣市交易筆數 inter_city_trans:int
跨縣市交易金額[新台幣] inter_city_amt:biginteger

原始資料集內容
 year    area  type  cards total_trans total_amt inter_city_trans inter_city_amt
2014-01,基隆市,ALL,241213,942118,2265105458,714100,1803194168
2014-02,基隆市,ALL,229540,813048,1842401862,641756,1533509566
2014-03,基隆市,ALL,239793,918036,1992896656,722421,1658553554
```

### 2018年哪一個縣市的跨縣市交易金額平均最高?
> pay = LOAD '/dataset/38315/38315.csv' USING PigStorage(',') AS (yaer: chararray,area:chararray,type:chararray,cards:chararray,total_trans:int,total_amt:biginteger, inter_city_trans:int, inter_city_amt:biginteger);
foreach_pay = FOREACH pay GENERATE SUBSTRING($0,0,4),$1,$6,$7;
filter_pay = FILTER foreach_pay BY $0 == '2018';
gp_pay = GROUP filter_pay BY $1;
avg_pay = FOREACH gp_pay GENERATE $0, SUM($1.$3)/SUM($1.$2);
desc_pay = ORDER avg_pay BY $1 DESC;
limit_pay = LIMIT desc_pay 1;
dump limit_pay;
```
(新竹市,4164)
```

### 總交易筆數中平均單筆消費金額最高的是哪個縣市?
> foreach_pay = FOREACH pay GENERATE $1,$4,$5;
gp_pay = GROUP foreach_pay BY $0;
sum_pay = FOREACH gp_pay GENERATE $0, SUM($1.$1),SUM($1.$2);
per_pay = FOREACH sum_pay GENERATE $0,$2/$1;
desc_pay = ORDER per_pay BY $1 DESC;
limit_pay = LIMIT desc_pay 1;
dump limit_pay;
```
(新竹市,2651)
```

## 999001 -- 連線紀錄
> connect = LOAD '/dataset/999001/999001.tsv' USING PigStorage('\t') AS (connection:int, type:chararray, protocol:chararray, service:chararray, timestamp:int, local_host:chararray, local_port:int, remote_host:chararray, remote_port:int);

```
欄位名稱
連線編號  connection:int
連線形式  type:chararray
通訊協定  protocol:chararray
服務程式  service:chararray
時間戳記  timestamp:int
本機位址  local_host:chararray
本機通訊埠  local_port:int
遠端位址  remote_host:chararray
遠端通訊埠  remote_port:int

原始資料集內容
connection  type  protocol  service  ctimestamp  local _host  local _port  remote_ host  remote_ port
3       accept  tcp     mssqld  1502196257      192.168.131.6   1433    222.174.114.42  56803
4       accept  tcp     mssqld  1502196259      192.168.131.6   1433    222.174.114.42  56889
5       accept  tcp     smbd    1502196284      192.168.131.4   445     218.81.136.101  2671
```

### 哪一個本機位址提供的服務程式種類最多？
> connect = LOAD '/dataset/999001/999001.tsv' USING PigStorage('\t') AS (connection:int, type:chararray, protocol:chararray, service:chararray, timestamp:int, local_host:chararray, local_port:int, remote_host:chararray, remote_port:int);
foreach_connect = FOREACH connect GENERATE $3,$5;
STORE foreach_connect INTO 'host.csv' USING PigStorage(',');
quit
hdfs dfs –get host.csv
cat host.csv | sort -t',' -k1,2 | uniq > toConnect.csv
(hdfs dfs –get 999001.tsv)
(cat 999001.tsv | cut -d $'\t' -f4,6 --output-delimiter="," | sort -t',' -k1,2 | uniq > toConnect.csv)
hdfs dfs –put toConnect.csv
pig
toConnect = LOAD 'toConnect.csv' USING PigStorage(',') AS(service:chararray , local_host:chararray);
gp_connect = GROUP toConnect BY $1;
count_connect = FOREACH gp_connect GENERATE $0, COUNT($1);
desc_connect = ORDER count_connect BY $1 DESC;
limit_connect = LIMIT desc_connect 1;
dump limit_connect;
```
(192.168.130.1,19)
```
### 哪一個服務程式的IP數最多？
> toConnect = LOAD 'toConnect.csv' USING PigStorage(',') AS(service:chararray , local_host:chararray);
gp_connect = GROUP toConnect BY $0;
count_connect = FOREACH gp_connect GENERATE $0, COUNT($1);
desc_connect = ORDER count_connect BY $1 DESC;
dump desc_connect; //觀察資料並列數量
Limit_connect = LIMIT desc_connect 10;
dump limit_connect;
```
(mysqld,10)
(mssqld,10)
(RtpUdpStream,10)
(SipSession,10)
(Blackhole,10)
(smbd,10)
(Memcache,10)
(httpd,10)
(upnpd,10)
(SipCall,10) 
```

### 哪一個遠端位址連線次數最多？
> connect = LOAD '/dataset/999001/999001.tsv' USING PigStorage('\t') AS (connection:int, type:chararray, protocol:chararray, service:chararray, timestamp:int, local_host:chararray, local_port:int, remote_host:chararray, remote_port:int);
foreach_connect = FOREACH connect GENERATE $0,$7;
gp_connect = GROUP foreach_connect BY $1;
count_connect = FOREACH gp_connect GENERATE $0, COUNT($1);
desc_connect = ORDER count_connect BY $1 DESC;
limit_connect = LIMIT desc_connect 1;
dump limit_connect; 
```
(35.185.109.141,31564)
```

## 999002 - 連線紀錄
> attack = LOAD '/dataset/999002/999002.tsv' USING PigStorage('\t') AS (download:int, connection:int, download_url:chararray, download_md5_hash:chararray);
```
欄位名稱
下載記錄編號 download:int
連線編號 connection:int
下載網址 download_url:chararray
下載檔案雜湊值 download_md5_hash:chararray

原始資料集內容
download  connection  download_url                       download_md5_hash
1       1220 http://118.89.159.61:12347/Se.exe       eccb44e2a6cb4ece00f17f2a56d918f4
2       1222 http://118.89.159.61:12347/svcyr.exe    0a2c841961c6b4b6b09a9bfc9a79a94c
3       1225 http://118.89.159.61:12347/Se.exe       eccb44e2a6cb4ece00f17f2a56d918f4
```

### 哪一個網址的IP:port被下載檔案最多次？
> foreach_attack = FOREACH attack GENERATE SUBSTRING($2,7,27),$3;
foreach_attack2 = FOREACH foreach_attack GENERATE STRSPLIT($0,'/',2),$1;
gp_attack = GROUP foreach_attack2 BY $0.$0;
count_attack = FOREACH gp_attack GENERATE $0,COUNT($1);
desc_attack = ORDER count_attack BY $1 DESC;
limit_attack = LIMIT desc_attack 1;
dump limit_attack;
```
(203.189.234.149:8080,282)
```
## 999001 跟 999002 均會使用到

### 哪一個遠端位址下載檔案次數最多？
> attack = LOAD '/dataset/999002/999002.tsv' USING PigStorage('\t') AS (download:int, connection:int, download_url:chararray, download_md5_hash:chararray);
foreach_connect = FOREACH connect GENERATE $0,$7;
foreach_attack = FOREACH attack GENERATE $1,$3;
join_connect_attack = JOIN foreach_connect BY $0, foreach_attack BY $0;
gp_connect_attack = GROUP join_connect_attack BY $1;
connect_attack = FOREACH gp_connect_attack GENERATE $0,COUNT($1);
desc_connect_attack = ORDER connect_attack BY $1 DESC;
limit_connect_attack = LIMIT desc_connect_attack 1;
dump limit_connect_attack;
```
(222.186.21.168,50)
```

### 哪一個本機位置被下載檔案次數第三多？
> attack = LOAD '/dataset/999002/999002.tsv' USING PigStorage('\t') AS (download:int, connection:int, download_url:chararray, download_md5_hash:chararray);
foreach_connect = FOREACH connect GENERATE $0,$5;
foreach_attack = FOREACH attack GENERATE $1,$3;
join_connect_attack = JOIN foreach_connect BY $0, foreach_attack BY $0;
gp_connect_attack = GROUP join_connect_attack BY $1;
connect_attack = FOREACH gp_connect_attack GENERATE $0,COUNT($1);
desc_connect_attack = ORDER connect_attack BY $1 DESC;
limit_connect_attack = LIMIT desc_connect_attack 3;
dump limit_connect_attack;
```
(192.168.130.3,87)
```
## 5989 跟 24333 均會使用到

### 哪個縣市的警察局與ATM數量差距最大？
> foreach_police = FOREACH police GENERATE $0,SUBSTRING($2,0,3);
gp_police = GROUP foreach_police BY $1;
count_police = FOREACH gp_police GENERATE $0,COUNT($1);
foreach_atm = FOREACH atm GENERATE $2,$3;
gp_atm = GROUP foreach_atm BY $1;
count_atm = FOREACH gp_atm GENERATE $0,COUNT($1);
replace_atm = FOREACH count_atm GENERATE REPLACE($0,'台北市','臺北市'),$1;
join_atm_police = JOIN replace_atm BY $0,count_police BY $0;
atm_police = FOREACH join_atm_police GENERATE $0,$1,$3;
atm_police2 = FOREACH atm_police GENERATE $0, $1/$2;
desc_police = ORDER atm_police2 BY $1 DESC;
limit_police = LIMIT desc_police 1;
```
(台北市,37)
```

## 26557 - 內政部行事曆
> holiday = LOAD '/dataset/26557/26557.csv' USING PigStorage(',') AS (year_day:chararray,holiday:chararray,week:int,why_holiday:chararray,who_holiday:chararray);
```
欄位名稱
年月日 year_day chararray
節日 holiday chararray
星期幾 week chararray
節慶說明 why_holiday chararray
誰放假 who_holiday chararray
```

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




