
## Oracle Summary 
### Pseudo-column
- Pseudo-Column(의사 컬럼)이란 Column처럼 동작 하지만, 실제로 Table에 저장되지 않는 Column을 의미한다. 
- SELECT 문에서는 Pseudo-Column을 사용할 수 있지만, 이 값을 INSERT, UPDATE, DELETE할 수 없다.    

**(1) CONNECT_BY_ISCYCLE, CONNECT_BY_ISLEAF, LEVEL**
- 계층형 Query에서 사용하는 Pseudo-Column 이다.  
- (추후 따로 정리 예정) 

**(2) NEXTVAL, CURRVAL**
- Sequence에서 사용하는 Pseudo-Column이다. 
- (추후 따로 정리 예정)

**(3) ROWNUM, ROWID** 
- ROWNUM은 Query에서 반환되는 각 Row에 대한 순서 값을 나타내는 Pseudo-Column이다.
```SQL
   SELECT ROWNUM, EMPLOYEE_ID
     FROM EMPLOYEES; 
```
```SQL
   SELECT ROWNUM, EMPLOYEE_ID, ROWID
     FROM EMPLOYEES 
    WHERE ROWNUM < 5;
```

- Table에 Data가 많으면 SELECT만 하더라도 결과가 나올 때까지 많은 시간이 소요된다.
- EMPLOYEES Table에 Column을 조회할 때 'SELECT * FROM EMPLOYEES'를 실행하면 전체 ROW의 확인까지 시간이 오래 걸리기 때문에 ROWNUM을 사용하면 편리하다. 
- ROWID 는 Table에 저장된 각 Row 저장된 유일한 값을 가리키는 Pseudo-Column이며, 각 Row를 식별하는 값이므로 ROWID는 유일한 값을 가진다.

### Operator   

**(1) 수식 연산자**
- 단항 연사자로 쓰일 때는 각각 ' + ', ' - '는  양수와 음수를 나타낸다.
- 이항 연산자로 사용될 때에는 ' + ', ' - ', ' * ', ' / '가 있다.   

**(2) 문자 연산자**
- '||'는 두 문자를 연결하는  연산을 수행한다. 
``` SQL 
    SELECT EMPLOYEE_ID  || '-' || EMP_NAME  AS EMPLOYEE_INFO
      FROM EMPLOYEES  
     WHERE ROWNUM < 5;
```
**(3) 논리 연산자** 
- 논리 연산을 수행하는 연산자로 수학에서 사용하는 부등호와 쓰임새는 같다. 
- 두 값이 같은지를 판단하는 등호(=)연산자의 반대인 비동등 연산자 '<>', '!=', '\^='가 존재하는데 이 세 연산자의 사용법과 반환 결과는 모두 동일하다. 
- 숫자 뿐만 아니라 문자와 날짜형도 비교가 가능하다. 

### Expression
- Expression (표현식)이란 한 개 이상의 값과 연산자, SQL 함수등이 결합된 식이다. 

**(1) CASE** 
```SQL
   SELECT EMPLOYEE_ID, SALARY, 
          CASE WHEN SALARY <= 5000 THEN 'C_GRADE'
               WHEN SALARY > 5000 AND SALARY <= 15000 THEN 'B_GRADE'
               ELSE 'A_GRADE'
           END AS SALARY_GRADE
     FROM EMPLOYEES; 
```

### Condition
- Condition(조건식)은 한 개 이상의 Expression(표현식)과 논리 연산자가 결합된 식으로 **TRUE**, **FALSE**, **UNKNOWN** 세 가지 타입을 반환한다.
- WHERE절에서 사용한 모든 모든 조건이 조건식에 포함된다. 

**(1) 비교 조건식**
- 논리 연산자, ANY, SOME, ALL Keyword로 비교하는 조건식을 말한다.   
  ① ANY
  - SALARY가 2000, 3000, 4000 증 하나라도 일치하는 모든 EMPLOYEE_ID를 조회 
```SQL
   SELECT EMPLOYEE_ID, SALARY 
     FROM EMPLOYEES 
    WHERE SALARY = ANY(2000, 3000, 4000)
    ORDER BY EMPLOYEE_ID ;
```
```SQL
   SELECT EMPLOYEE_ID, SALARY 
     FROM EMPLOYEES
    WHERE SALARY = 2000
       OR SALARY = 3000
       OR SALARY = 4000;
```
  ② ALL    
     - ALL은 모든 조건을 동시에 만족해야 하지만, SALARY는 한 가지 값만 가지고 있으므로 논리적으로 잘못된 Query이다. 
```SQL
   SELECT EMPLOYEE_ID , SALARY 
     FROM EMPLOYEES e 
    WHERE SALARY = ALL(2000, 3000, 4000)
    ORDER BY EMPLOYEE_ID
```
 ③ SOME
 ```SQL
 
 ```
  
