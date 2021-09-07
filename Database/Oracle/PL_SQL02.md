## Oracle PL_SQL Chapter02
### PL/SQL Procedure
**(1) PL/SQL Exception** 
- PL/SQL 코드를 작성할 때 발생할 수 있는 오류에는 크게 두가지로 나뉜다. 첫 번째는 문법오류로 객체 (Table, View, Function, Procedure)나 키워드 이름을 잘못 참조하거나, Function, Procedure의 Parameter를 잘못 명시했을 때 발생되는 오류로 이들은 Compile할때 걸러진다. 두 번째는 Compile할 때는 아무 문제가 없으나 Runtime 때 로직을 처리하면서 발생하는 오류인데 이를 Exception이라고 한다. 
- Exception은 Oracle에서 발생시키는 **System Exception**, 사용자가 의도적으로 발생시킬 수 있는 **User Defined Exception**으로 나뉜다. 
```SQL 
   EXCEPTION WHEN EXCEPTION_NAME THEN 예외처리구문1 
             WHEN EXCEPTION_NAME THEN 예외처리구문2
             ...
             WHEN EXCEPTION_NAME THEN 예외처리구문N;
```
- WHEN 다음에 위치하는 예외처리 구문은 아무 이름이나 사용할 수 없고, 시스템 예외 중 일부와 사용자가 직접 정의한 예외명을 사용할 수 있다.
- 만약 구체적인 예외명을 알 수 없다면 **OTHERS**를 사용하면 되는데 이렇게 하면 Oracle 시스템에서 PL/SQL 코드 상 발생한 Runtime Exception을 자동으로 잡아준다. 
```SQL
   DECLARE 
    vi_num NUMBER :=0;
    BEGIN 
      vi_num:= 10/0;
      DBMS_OUTPUT.PUT_LINE('SUCCESS');
    END;
```
```SQL
   DECLARE 
    vi_num NUMBER :=0;
    BEGIN  
      vi_num := 10/0 ;
      DBMS_OUTPUT.PUT_LINE('SUCCESS');
      EXCEPTION WHEN OTHERS THEN
         DBMS_OUTPUT.PUT_LINE('ERROR');
    END;
 ```

```SQL
   CREATE OR REPLACE PROCEDURE TEST_NO_EXCEPTION_PROC
   IS
    vi_num NUMBER := 0;
    BEGIN 
      vi_num :=10/0;
      DBMS_OUTPUT.PUT_LINE('SUCCESS');
    END;
```
```SQL
   CREATE OR REPLACE PROCEDURE TEST_EXCEPTION_PROC
   IS
     vi_num NUMBER :=10;
     BEGIN 
       vi_num :=10/0;
       DBMS_OUTPUT.PUT_LINE('SUCCESS');
       EXCEPTION WHEN OTHERS THEN
         DBMS_OUTPUT.PUT_LINE('ERROR');
     END;
```
**(2) PL/SQL SQLCODE, SQLERRM**
- TEST_EXCEPTION_PROC Procedure에서 피제수를 0으로 나눈 후 예외가 발생했을 때 단순히 메시지를 출력하기 보다는 어떤 오류가 발생했는지 알고 있을 때 Oracle에서는 발생한 예외 정보를 참조하기 위한 수단으로 **SQLCODE** 와 **SQLERRM**이란 Built-in Function을 제공하고 있다.    
- **SQLCODE** 
   - 실행부에서 발생한 예외에 해당하는 코드를 반환한다. 예를 들어 0으로 나누면 이에 대한 예외 코드인 '-1476'을 반환한다. 에러 없이 성공하면 '0'을 반환한다.
- **SQLERRM**
   - 발생한 예외에 대한 오류 메시지를 반환한다. 이 함수는 매개변수로 예외코드 값을 받는데, 매개변수를 넘기지 않으면 Default로 SQLCODE가 반환한 예외코드 값과 연관된 예외 메시지를 반환한다. 
- **DBMS_UTILITY.FORMAT_ERROR_BACKTRACE**
   - DBMS_UTILITY.FORMAT_ERROR_BACKTRACE를 활용하면 몇번째 줄에서 예외가 발생했는지를 확인 가능하다. 
- **DBMS_UTILITY.FORMAT_CALL_STACK**
   - DBMS_UTILITY.FORMAT_CALL_STACK를 활용하면 발생한 예외에 대한 자세한 정보를 확인 가능하다. 

```SQL 
   CREATE OR REPLACE PROCEDURE TEST_EXCEPTION_PROC
   IS
    vi_num NUMBER :=10;
    BEGIN 
      vi_num :=10/0;
      DBMS_OUTPUT.PUT_LINE('SUCCESS');

      EXCEPTION WHEN OTHERS THEN
        DBMS_OUTPUT.PUT_LINE('ERROR');
        DBMS_OUTPUT.PUT_LINE('SQL ERROR CODE:'||SQLCODE);
        DBMS_OUTPUT.PUT_LINE('SQL ERROR MESSAGE :'||SQLERRM);
        DBMS_OUTPUT.PUT_LINE(SQLERRM(SQLCODE));
        DBMS_OUTPUT.PUT_LINE('ERROR LINE'||DBMS_UTILITY.FORMAT_ERROR_BACKTRACE);
        DBMS_OUTPUT.PUT_LINE('ERROR LINE : '||DBMS_UTILITY.FORMAT_CALL_STACK);
    END;
```    
