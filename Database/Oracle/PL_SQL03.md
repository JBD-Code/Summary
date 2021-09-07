## Oracle PL_SQL Chapter03
### PL/SQL User Defined Exception
**(1) PL/SQL User Defined Exception** 
- Oracle에서는 사용자가 직접 예외를 정의해서 사용할 수 있다. 
- 사용자 정의 예외를 사용하려면 변수, 상수처럼 PL/SQL 블록의 선언부에서 예외를 정의해야한다. 
- 시스템 예외는 자동으로 검출되지만, 사용자 예외는 직접 예외를 발생시켜야 하는데 "RAISE 사용자 정의 예외명" 형태로 사용한다. 
- 예외를 발생 시키면 자동으로 제어권이  EXCEPTION 절로 넘어오므로 시스템예외와 동일한 방식으로 처리해주면 된다. 
```SQL
   CREATE OR REPLACE PROCEDURE TEST_USER_EXCEPTION
    (
     p_emp_name EMPLOYEES.EMP_NAME%TYPE,
     p_department_id DEPARTMENTS.DEPARTMENT_ID%TYPE
    ) IS 
     vn_employee_id EMPLOYEES.EMPLOYEE_ID%TYPE;
     vd_curr_date   DATE := SYSDATE;
     vn_cnt         NUMBER := 0;

     ex_invalid_depid EXCEPTION;

     BEGIN
      SELECT COUNT(*)
        INTO vn_cnt
        FROM DEPARTMENTS
       WHERE DEPARTMENT_ID = p_department_id; 

       IF vn_cnt = 0 THEN
         RAISE ex_invalid_depid;
       END IF;

         SELECT MAX(EMPLOYEE_ID)+1
           INTO vn_employee_id 
           FROM EMPLOYEES;

         INSERT INTO EMPLOYEES
          (
           EMPLOYEE_ID,
           EMP_NAME,
           HIRE_DATE,
           DEPARTMENT_ID
          )
          VALUES   
          (
           vn_employee_id,
           p_emp_name,
           vd_curr_date,
           p_department_id
          );
          COMMIT;

          EXCEPTION 
            WHEN ex_invalid_depid THEN
                 DBMS_OUTPUT.PUT_LINE('ERROR');
            WHEN OTHERS THEN     
                 DBMS_OUTPUT.PUT_LINE('ERROR CODE : '||SQLCODE);
                 DBMS_OUTPUT.PUT_LINE('ERROR MESSAGE : '||SQLERRM);
                 DBMS_OUTPUT.PUT_LINE('ERROR LINE : '||DBMS_UTILITY.FORMAT_ERROR_BACKTRACE);
     END;        
```

**(2) RAISE, RAISE_APPLICATION_ERROR**   
 - 사용자 정의 예외를 명시적, 의도적으로 발생시키기 위해서 "RAISE 사용자 정의 예외명"을 사용하지만 대신에 미리 정의된 예외명을 명시해서 사용하는 것도 가능하다.  
```SQL
   CREATE OR REPLACE PROCEDURE TEST_USER_EXCEPTION2
    (
     p_num NUMBER 
     ) IS

     BEGIN 
       IF  p_num <= 0 THEN 
         RAISE INVALID_NUMBER;
       END IF ;

       DBMS_OUTPUT.PUT_LINE(p_num);

       EXCEPTION 
         WHEN INVALID_NUMBER THEN
           DBMS_OUTPUT.PUT_LINE('ERROR');
         WHEN OTHERS THEN
           DBMS_OUTPUT.PUT_LINE('ERROR CODE : '||SQLCODE);
           DBMS_OUTPUT.PUT_LINE('ERROR MESSAGE : '||SQLERRM);
           DBMS_OUTPUT.PUT_LINE('ERROR LINE : '||DBMS_UTILITY.FORMAT_ERROR_BACKTRACE);
     END;
```
