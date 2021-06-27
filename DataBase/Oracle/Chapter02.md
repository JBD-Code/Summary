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
       COLUMNS1, LENGTH(COLUMNS1) AS len1 , 
       COLUMNS2, LENGTH(COLUMNS1) AS len2
    FROM EX2_1;

   SELECT 
     COLUMNS3, LENGTH(COLUMNS3) AS LENGTH3, LENGTHB(COLUMNS3) AS BYTELENGTH3 
   FROM EX2_2;

```

