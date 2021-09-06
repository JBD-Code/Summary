## Oracle PL_SQL Chapter01
### PL/SQL Procedure
**(1) PL/SQL Procedure** 
- Function은 특정 연산을 수행한 뒤 결과값을 반환하지만 Procedure는 특정한 로직을 처리하기만 하고 결과값을 반환하지 않는다.
- Procedure는 Database에 저장된 Object이므로 Procedure를 Stored Procedure라고 한다. 

```SQL 
   CREATE OR REPLACE Procedure Procedure_Name 
   (
    Parameter_Name1[IN||OUT||IN OUT] DATATYPE[:= Default Value],
    Parameter_Name2[IN||OUT||IN OUT] DATATYPE[:= Default Value],
   )
   IS[]AS
   RETURN DATATYPE;
   IS[AS]
    Variable, Constant Declaration
    BEGIN
      [실행부]
      RETURN Value
    EXCEPTION
      [예외 처리부]
    END Procedure_Name 
```
- CREATE OR REPLACE FUNCTION : CREATE OR REPLACE 구문을 사용해서 Procedure을 생성한다. 
- Parameter : IN은 입력, OUT는 출력, IN OUT은 입/출력을 동시에 한다. 아무 것도 명시하지 않으면 Default Value로 IN을 의미한다. 
```SQL
CREATE OR REPLACE PROCEDURE MY_NEW_JOB_PROC
 (
   P_JOB_ID    IN JOBS.JOB_ID%TYPE,
   P_JOB_TITLE IN JOBS.JOB_TITLE%TYPE,
   P_MIN_SAL   IN JOBS.MIN_SALARY%TYPE,
   P_MAX_SAL   IN JOBS.MAX_SALARY%TYPE
  ) IS
  
  BEGIN 
    INSERT INTO JOBS
    (
     JOB_ID, 
     JOB_TITLE, 
     MIN_SALARY, 
     MAX_SALARY, 
     CREATE_DATE,
     UPDATE_DATE
     )
    VALUES
    (
     P_JOB_ID, 
     P_JOB_TITLE,
     P_MIN_SAL,
     P_MAX_SAL,
     SYSDATE,
     SYSDATE
     );
     COMMIT;
  END;
```
**(2) PL/SQL Procedure Execution**
- Function은 반환값을 받으므로 실행할 때 '호출'이라고 명명하지만 Procedure는 '호출', '실행'한다고 표현한다. 
- Procedure는 반환값이 없으므로 Function 처럼 SELECT 절에는 사용할 수 없다. 
```SQL
   EXEC|| EXECUTE Procedure Name (Parameter1, Parameter2, ...); 
```
```SQL
   BEGIN
     Procedure Name(Parameter1, Parameter2, ...);
   END;   
```
```SQL
CREATE OR REPLACE PROCEDURE MY_NEW_JOB_PROC
 (
   P_JOB_ID    IN JOBS.JOB_ID%TYPE,
   P_JOB_TITLE IN JOBS.JOB_TITLE%TYPE,
   P_MIN_SAL   IN JOBS.MIN_SALARY%TYPE,
   P_MAX_SAL   IN JOBS.MAX_SALARY%TYPE
  ) IS
  vn_cnt NUMBER :=0; 
  
  BEGIN  
    SELECT COUNT(*)
      INTO vn_cnt
      FROM JOBS
     WHERE JOB_ID = P_JOB_ID;
     
     IF vn_cnt = 0 THEN
        INSERT INTO JOBS
        (
         JOB_ID, 
         JOB_TITLE, 
         MIN_SALARY, 
         MAX_SALARY, 
         CREATE_DATE,
         UPDATE_DATE
         )
        VALUES
        (
         P_JOB_ID, 
         P_JOB_TITLE,
         P_MIN_SAL,
         P_MAX_SAL,
         SYSDATE,
         SYSDATE
         );
     ELSE 
        UPDATE JOBS
           SET JOB_TITLE   = P_JOB_TITLE,
               MIN_SALARY  = P_MIN_SAL,
               MAX_SALARY  = P_MAX_SAL, 
               UPDATE_DATE = SYSDATE
         WHERE JOB_ID = P_JOB_ID;
    END IF;
    COMMIT; 
   END;   
```
```SQL
   BEGIN 
     MY_NEW_JOB_PROC (P_JOB_ID => 'SM_JOB2', P_JOB_TITLE => 'SAMPLE JOB2', P_MIN_SAL =>3000, P_MAX_SAL => 7000);  
   END ;  
```
**(3) PL/SQL Procedure OUT, IN OUT**
- Procedure와 Function 의 가장 큰 차이점은 반환 값의 존재여부이다. 
- Procedure에서도 반환하는 방법이 있는데 바로 OUT 매개 변수를 통해서 실현할 수 있다. 
- OUT 매개변수란 Procedure 실행 시점에 OUT 매개변수를 변수 형태로 전달하고 Procedure 실행부에서 이 매개변수에 특정값을 할당한다. 

```SQL
   CREATE OR REPLACE PROCEDURE MY_NEW_JOB_PROC
    (
      P_JOB_ID    IN JOBS.JOB_ID%TYPE,
      P_JOB_TITLE IN JOBS.JOB_TITLE%TYPE,
      P_MIN_SAL   IN JOBS.MIN_SALARY%TYPE,
      P_MAX_SAL   IN JOBS.MAX_SALARY%TYPE,
      P_UPD_DATE  OUT JOBS.UPDATE_DATE%TYPE
     ) IS
     vn_cnt NUMBER :=0; 
     vn_cur_date JOBS.UPDATE_DATE%TYPE :=SYSDATE;

     BEGIN  
       SELECT COUNT(*)
         INTO vn_cnt
         FROM JOBS
        WHERE JOB_ID = P_JOB_ID;

        IF vn_cnt = 0 THEN
           INSERT INTO JOBS
           (
            JOB_ID, 
            JOB_TITLE, 
            MIN_SALARY, 
            MAX_SALARY, 
            CREATE_DATE,
            UPDATE_DATE
            )
           VALUES
           (
            P_JOB_ID, 
            P_JOB_TITLE,
            P_MIN_SAL,
            P_MAX_SAL,
            vn_cur_date,
            vn_cur_date
           );
        ELSE 
          UPDATE JOBS
             SET JOB_TITLE   = P_JOB_TITLE,
                 MIN_SALARY  = P_MIN_SAL,
                 MAX_SALARY  = P_MAX_SAL, 
                 UPDATE_DATE = vn_cur_date
           WHERE JOB_ID = P_JOB_ID;
      END IF;
      
      P_UPD_DATE := vn_cur_date; 
      COMMIT; 
     END;       
```
