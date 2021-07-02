
## Oracle Summary 00 
### SELECT 

**(1) SELECT** 
- SQL에 대한 사전지식이 없다고 가정하고 Data를 조회할 경우에 필요한 것은 어디에서 (WHERE) , 어떤 Data를 가져올 것인지로 구분할 수 있다. 
- 이 때 '어디에서'에 해당하는 내용을 Table, View를 FROM 절에서, '어떤 Data'에 해당하는내용을 SELECT 절에서 기술해 줄 수 있다. 
- '어떤 Data'는 다시 어떠한 조건에 맞는 Data를 식별해야 하는데 이 조건을 기술하는 절이 WHERE 절에 해당한다.

```SQL
  SELECT EMPLOYEE_ID, EMP_NAME
    FROM EMPLOYEES 
   WHERE SALARY > 5000;
```

```SQL
  SELECT COUNT(*)
   FROM EMPLOYEES 
  WHERE SALARY > 5000;
```

```SQL
  SELECT EMPLOYEE_ID, EMP_NAME
   FROM EMPLOYEES 
  WHERE SALARY > 5000
    AND JOB_ID LIKE '%IT_PROG%'
  ORDER BY EMPLOYEE_ID;
```

```SQL
  SELECT EMPLOYEE_ID, EMP_NAME
   FROM EMPLOYEES 
  WHERE SALARY > 5000
     OR JOB_ID LIKE '%IT_PROG%'
  ORDER BY EMPLOYEE_ID;
```
- FROM절을 보면 Table 다음에 A, B를 명시하고 SELECT, WHERE 절에서 A.Column, B.Column형태로 사용하는데 A, B를 **ALIAS**라고 한다. 
- Table 뿐만 아니라 Column에도 붙일 수 있으 AS는 생략이 가능하다. 
- SELECT, WHERE 절에서 Column을 명시하려면 'Table.Column' 형태로 써야하는데 Table Name이 길면 SQL 문장도 길어지기 때문에 가독성이 떨어지기 때문에 이러한 경우 ALIAS을 만들어 사용하면 편리하다. 
```SQL
  SELECT A.EMPLOYEE_ID, 
         A.EMP_NAME , 
         A.DEPARTMENT_ID,
         B.DEPARTMENT_ID
    FROM EMPLOYEES A,
         DEPARTMENTS B
   WHERE A.DEPARTMENT_ID = B.DEPARTMENT_ID;

```
**(2) INSERT**
- 신규로 Data를 입력 할 때는 INSERT 문을 이용한다.  
- 나열하는 Column과 값과 순서 그리고 Data Type이 일치해야 하며, 일치하지 않을 경우 오류가 발생한다. 

```SQL
  INSERT INTO EX3_1 (COL1, COL2, COL3 ) VALUES ('ABC', 10, SYSDATE);
  INSERT INTO EX3_1 VALUES('DEF', 20, SYSDATE);
```

```SQL
   INSERT INTO EX3_2 
   VALUE 
        (
          SELECT EMPLOYEE_ID, EMP_NAME
            FROM EMPLOYEES 
           WHERE SALARY >5000
        );
```
  

**(3) UPDATE** 
- Table에 있는 기존의 Data를 수정할 대 사용하는 문장이 UPDATE이다.

```SQL
    UPDATE EX3_1
       SET COL1 = 'ABD'
     WHERE COL1 = 'ABC';
```
**(4) MERGE**
- MERGE문은 조건을 비고ㅛ해서 Table에 해당 조건에 맞는 Data가 없으면 INSERT, 있으면 UPDATE를 수행하는 문장이다 
```SQL
   INSERT INTO EX3_3 (EMPLOYEE_ID)
   SELECT A.EMPLOYEE_ID 
     FROM EMPLOYEES A, 
          SALES S
    WHERE A.EMPLOYEE_ID  = S.EMPLOYEE_ID
      AND S.SALES_MONTH BETWEEN  '200010' AND '200012'
    GROUP BY A.EMPLOYEE_ID ;
```
```SQL 
   
   SELECT EMPLOYEE_ID, MANAGER_ID, SALARY, SALARY * 0.01
     FROM EMPLOYEES 
    WHERE EMPLOYEE_ID IN 
              ( 
                SELECT EMPLOYEE_ID 
                FROM EX3_3
              );
              
```

```SQL
   MERGE INTO EX3_3 D 
   USING 
        (
          SELECT EMPLOYEE_ID, 
                 SALARY,
                 MANAGER_ID 
            FROM EMPLOYEES 
           WHERE MANAGER_ID = 146
        ) B 
      ON (D.EMPLOYEE_ID = B.EMPLOYEE_ID) 
    WHEN MATCHED THEN UPDATE SET D.BONUS_AMT = D.BONUS_AMT + B.SALARY * 0.01
    WHEN NOT MATCHED THEN INSERT (D.EMPLOYEE_ID, D.BONUS_AMT)
                          VALUES (B.EMPLOYEE_ID, B.SALARY *0.01) 
                           WHERE (B.SALARY < 8000);
```  

**(5) DELETE**
- Table에 있는 Data를 삭제할 때 DELETE문을 사용한다. 
```SQL
   DELETE EX3_3;
```
