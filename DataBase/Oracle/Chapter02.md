## Oracle Query
### Table 

#### (1) CREATE

```SQL
    CREATE TABLE EX2_1 
    (
     COLUMNS1  CHAR(10),
     COLUMNS2  VARCHAR2(10),
     COLUMNS3  NVARCHAR2(10),
     COLUMNS4  NUMBER
    );
    
    CREATE TABLE EX2_2
    (
     COLUMNS1 VARCHAR(3),
     COLUMNS1 VARCHAR(3 byte),
     COLUMNS1 VARCHAR(3 char)
    );
``` 

#### (2) INSERT
```SQL
   INSERT INTO EX2_1 
     ( 
      COLUMNS1 , 
      COLUMNS2
     )
   VALUES 
     (
      'abc', 
      'abc'
     );
      
   INSERT INTO EX2_2 VALUES ('abc', 'abc', 'abc');
   INSERT INTO EX2_2 (column3) VALUES ('홍길동');
```

#### (3) SELECT 
```SQL
   SELECT 
       COLUMNS1, LENGTH(COLUMNS1) AS LEN1 , 
       COLUMNS2, LENGTH(COLUMNS1) AS LEN2
    FROM EX2_1;
```
 - 가변길이와 고정길이의 차이   

|COLUMNS1|LEN1|COLUMN2|LEN2|
|------|---|---|---|
|abc| 10| abc|3 |

```SQL

   SELECT 
     COLUMNS3, LENGTH(COLUMNS3) AS LENGTH3, LENGTHB(COLUMNS3) AS BYTELENGTH3 
   FROM EX2_2;
```
 - 컬럼 타입을 선언할 때 (숫자)만 명시하면 디폴트 값인 byte가 적용된다 
 - 영어는 한 문자를 1byte로 한글은 2byte를 차지하지만, 한글의 경우 무조건 2byte가 아니며 데이터베이스 설정에 따라 3byte를 차지하기도 한다.   
    
|COLUMNS3|LENGTH3|BYTELENGTH3|
|------|---|---|
|abc| 3| 3|
|홍길동| 3 |9|

