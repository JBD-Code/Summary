## Oracle Query
### Table 

#### ① CREATE EX2_1 

```SQL
   CREATE TABLE EX2_1 
    (
     COLUMNS1  CHAR(10),
     COLUMNS2  VARCHAR2(10),
     COLUMNS3  NVARCHAR2(10),
     COLUMNS4  NUMBER
    );
``` 
#### ② INSERT EX2_1 

```SQL
   INSERT INTO EX2_1 (COLUMNS1, COLUMNS2) VALUES('abc', 'abc');
```

#### ③ SELECT EX2_1 
```SQL
   SELECT COLUMNS1, 
          LENGTH(COLUMNS1) AS LEN1, 
          COLUMNS2, 
          LENGTH(COLUMNS1) AS LEN2
     FROM EX2_1;
```
 - 가변길이와 고정길이의 차이   

|COLUMNS1|LEN1|COLUMN2|LEN2|
|------|---|---|---|
|abc| 10| abc|3 |

#### ① CREATE EX2_2

```SQL
   CREATE TABLE EX2_2
    (
     COLUMNS1 VARCHAR(3),
     COLUMNS1 VARCHAR(3 byte),
     COLUMNS1 VARCHAR(3 char)
    );
``` 
#### ② INSERT EX2_2

```SQL   
   INSERT INTO EX2_2 VALUES ('abc', 'abc', 'abc');
   INSERT INTO EX2_2 (column3) VALUES ('홍길동');
```

#### ③ SELECT EX2_2

```SQL
   SELECT COLUMNS3, 
          LENGTH(COLUMNS3) AS LENGTH3, 
          LENGTHB(COLUMNS3) AS BYTELENGTH3 
     FROM EX2_2;
```
 - Column Type을 선언할 때 (숫자)만 명시하면 Default 값인 byte가 적용된다 
 - 영어는 한 문자를 1byte로 한글은 2byte를 차지한다.
 - 한글은 무조건 2byte가 아니며 설정에 따라 3byte를 차지하기도 한다.   
    
|COLUMNS3|LENGTH3|BYTELENGTH3|
|------|---|---|
|abc| 3| 3|
|홍길동| 3 |9|

#### ① CREATE EX2_3

```SQL
   CREATE TABLE EX2_3 
   (
    COL_DATE DATE,
    COL_TIMESTAMP TIMESTAMP
   );
 
``` 
#### ② INSERT EX2_3

```SQL   
  INSERT INTO EX2_3 VALUES (SYSDATE, SYSTIMESTAMP);
  INSERT INTO EX2_3 VALUES (SYSDATE, SYSTIMESTAMP);
```

#### ③ SELECT EX2_3

```SQL
   SELECT * 
     FROM EX2_3
```
|COL_DATE|COL_TIMESTAMP|
|------|---|
|2021-06-27 16:19:57|2021-06-27 16:19:57|
|2021-06-27 16:22:34|2021-06-27 16:22:34|

