## Oracle PL_SQL Chapter05
### PL/SQL Cursor
**(1) PL/SQL Cursor** 
- SQL의 가장 큰 특징은 Data를 집합적, 일괄적으로 처리한다는 것이다.  Row를 하나씩 개별적으로 처리하기 보다는 특정 조건에 맞는 Row를 선별해서 한꺼번에 처리한다. 
- Procedure를 개발하다 보면 Data를 한 개의 Row씩 처리해야 하는 상황이 발생하는 데 이때 Cursor를 이용한다. 
- 특정 SQL문을 처리한 결과를 담고 있는 영역(Private memory area)을 가리키는 일종의 Point로, Cursor를 사용하면 처리된 SQL문의 결과 집합에 접근이 가능하다. 
- SQL문은 집합적 언어이므로 임의의 SQL문이 처리된 결과의 Row 수는 한 개 이상인데 Cursor을 사용해 개별 Row에 순차적으로 접근이 가능하다.   
- Implicit cursor, Explicit cursor에 관계없이 open - fetch - close 3단계로 진행된다. 

**(2) 묵시적 커서(Implicit cursor)**
- Oracle내부에서 자동으로 생성되어 사용하는 Cursor, SQL문(INSERT, UPDATE, MERGE, DELETE, SELECT INTO)이 실행될 때 마다 자동으로 만들어지고 사용된다. 
- 개발자의 입장에서는 이러한 Cursor의 동작에 관여할 수는 없지만, Cursor 속성을 이용하면 여러가지 정보를 얻어낼 수 있다.   

|속성명|속성 설명|
|-----|--------|
|SQL%FOUND| 결과 집합의 Fetch row 수가 1개 이상이면 TRUE, 아니면 FALSE를 반환한다.|
|SQL%NOTFOUND| 결과 집합의 Fetch row 수가 0이면 TRUE, 아니면 FALSE를 반환한다.|
|SQL%ROWCOUNT| 영향 받은 결과 집합의 Row수를 반환, 없으면 0을 반환한다.|
|SQL%ISOPEN|Implicit cursor 는 항상 FALSE를 반환|

```SQL
   DECLARE 
     vn_department_id EMPLOYEES.department_id%TYPE :=80;

     BEGIN 
       UPDATE EMPLOYEES 
          SET EMP_NAME = EMP_NAME 
        WHERE DEPARTMENT_ID = vn_department_id; 
        
        DBMS_OUTPUT.PUT_LINE(SQL%ROWCOUNT); 
      COMMIT;
    END;
```
**(3) 명시적 커서(Explicit cursor)**
- 사용자가 직접 정의해서 사용하는 Cursor을 의미한다. 
- Explicit cursor를 사용하기 위해서는 Cursor 선언 - Cursor 열기 - Fetch 단계에서 Cursor 사용 - Cursor close 4단계로 진행된다.    
- **Cursor 선언**
  - 묵시적 커서와 달리 명시적 커서는 사용할 커서를 선언부에 직접 정의한다. 명시적 커서란 결과 Data 집합을 Row별로 참조해서 무언가 작업을 하기 위한 용도이므로 당연히 Cursor을 사용하는 문장은 SELECT문이다.  
  - CURSOR_NAME는 사용자가 직접정의, PARAMETER 생략가능한데, 생략하지 않는다면 이들은 SELECT문장의 WHERE 절에서 조건을 확인하는 용도로 사용된다. 
  ```SQL
     CURSOR Cursor_Name[Parameter1, Parameter2, ...];
     IS
     SELECT 
  ```
- **Cursor 열기**
  - Cursor을 선언 후 해당 Cursor을 사용하려면 먼저 Cursor을 열어야 한다. 
  ```SQL
     OPEN Cursor_Name[Parameter1, Parameter2, ...];
  ```
- **Fetch 단계에서 Cursor 사용**  
  - 선언한 Cursor을 열고 난 후 SELECT문의 결과로 반환되는 Row에 접근이 가능하다. Row의 수는 1개 이상이므로 개별 Row에 접근하기 위해서는 반복문(LOOP, WHILE, FOR)문을 사용한다. 
  - FETCH...INFO 를 통해 반환되는 각 Columns 값을 Parameter에 할당이 가능하다. 이때 Parameter의 수는 반환된 Column의 수와 일치해야 한다. 
  ```SQL
     LOOP
      FETCH Cursor_Name INTO Parameter1, Parameter2,...;
      EXIT WHEN Cursor_Name%NOTFOUND; 
     EXIT LOOP;  
  ```
- **Cursor 닫기**
  - Fetch 작업이 끝나고 반복문을 빠져 나오면 Cursor 사용이 모두 끝났으므로 반드시 Cursor을 닫아야 한다. 
   ```SQL
      CLOSE Cursor_Name 
   ```

```SQL
   DECLARE 
   vs_emp_name EMPLOYEES.EMP_NAME%TYPE;


   CURSOR cur_emp_dep(cp_department_id EMPLOYEES.department_id%TYPE)
   IS
   SELECT EMP_NAME
     FROM EMPLOYEES 
    WHERE DEPARTMENT_ID = cp_department_id; 

   --CURSOR 열기 
   BEGIN 
     OPEN cur_emp_dep(90);
     --반목분을 통한 FETCH 작업 
       LOOP
        FETCH cur_emp_dep INTO vs_emp_name; 

         EXIT WHEN cur_emp_dep%NOTFOUND;

         DBMS_OUTPUT.PUT_LINE(vs_emp_name);
       END LOOP;
     --CURSOR 닫기 
     CLOSE cur_emp_dep;
    END;    
```
