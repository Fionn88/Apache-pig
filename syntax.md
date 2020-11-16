# 金象盃比賽

## PIG
### FILTER
> FILTER 變數 BY 欄位 條件

EX:
- 顯示藥局為丁丁藥局
```
a1 = FILTER data BY $1 == '丁丁藥局';
```
- 顯示藥局不為丁丁藥局
```
a1 = FILTER data BY $1 != '丁丁藥局';
```

> FILTER 變數 BY 欄位 MATCHES .*

EX:
- 顯示地址有包含臺北市的資料
```
a1 = FILTER data BY $2 MATCHES '臺北市.*';
```
- 顯示地址有包含中正路的資料
```
a1 = FILTER data BY $2 MATCHES '.*中正路.*';
```
### REPLACE
> FOREACH 變數 GENERATE REPLACE(欄位,被替換的字,要替換的字)

EX:
- 替換第二個欄位桃園縣變桃園市
```
a1 = FOREACH data GENERATE REPLACE($2,'桃園縣','桃園市');
```
### SUBSTRING
> FOREACH 變數 GENERATE SUBSTRING(欄位2,起點位置,結束位置)

EX:
- 顯示地址的第1 ~ 3 個字
```
a1 = FOREACH data GENERATE SUBSTRING($2,0,3);
```
- 顯示地址的第4 ~ 6 個字
```
a1 = FOREACH data GENERATE SUBSTRING($2,3,6);
```
### GROUP
> GROUP 變數 ALL

EX:
- 將所有資料分在同一組
```
a1 = GROUP data ALL;
```
### COUNT
> FOREACH 分組後的變數 GENERATE 分組條件, COUNT(被分組的變數) 

EX:
- 計算資料總共有幾筆
```
a2 = FOREACH a1 GENERATE $0, COUNT($1);
```
### DISTINCT
> DISTINCT 變數

EX:

- 去除重複的資料
```
a1 = DISTINCT data;
```
### STRSPLIT
> FOREACH 變數 GENERATE STRSPLIT($2,'-',2),$9;

- 分割第三欄位，以 '-' 分割，分為兩欄
```
foreach_farm = FOREACH farm GENERATE STRSPLIT($2,'-',2),$9;

((香水百合,香水百合),43)
((香水百合,多朵),12)
((香水百合,紅雙朵),44)
```


### JOIN
> JOIN 變數1 BY 變數1欄位, 變數2 BY 變數2欄位

EX:
- 使用 JOIN 將縣市相同的資料合併, 輸出範例為 : (臺北市,614, 臺北市,1566182)

```
c1 = JOIN a2 BY $0, b2 BY $0;
```

### STORE
> STORE 變數 INTO 'new_csv.csv' using PigStorage(',');

## bash script

### --output-delimiter=","
- tab分割檔案改用,分隔
> cat 檔案 | cut -d $'\t' -f1-10 --output-delimiter=","

### cut
- 使用 cut命令取出每筆資料的前三個字
> cat twmask2.csv |  cut -d',' -f3 | cut -c1-9

### uniq
- uniq 命令會檢查每一行與下一行是否重複，若重複則刪除一行
> cat twmask2.csv |  cut -d',' -f3 | cut -c1-9 | uniq

### sort
- 使用 sort 命令排序成人口罩剩餘數
> cat twmask2.csv |sort -t',' -k5




 