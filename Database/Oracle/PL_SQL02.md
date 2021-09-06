## Oracle PL_SQL Chapter02
### PL/SQL Procedure
**(1) PL/SQL Exception** 
- PL/SQL 코드를 작성할 때 발생할 수 있는 오류에는 크게 두가지로 나뉜다. 첫 번째는 문법오류로 객체 (Table, View, Function, Procedure)나 키워드 이름을 잘못 참조하거나, Function, Procedure의 Parameter를 잘못 명시했을 때 발생되는 오류로 이들은 Compile할때 걸러진다. 두 번째는 Compile일 때는 아무 문제가 없으나 Runtime 때 로직을 처리하면서 발생하는 오류인데 이를 Exception이라고 한다. 
- Exception은 Oracle에서 발생시키는 **System Exception**, 사용자가 의도적으로 발생시킬 수 있는 **User Defined Exception**으로 나뉜다. 
```SQL 
   EXCEPTION WHEN EXCEPTION_NAME THEN 예외처리구문1 
             WHEN EXCEPTION_NAME THEN 예외처리구문2
             ...
             WHEN EXCEPTION_NAME THEN 예외처리구문N;
```
- WHEN 다음에 위치하는 예외처리 구문은 아무 이름이나 사용할 수 없고, 시스템 예외 중 일부와 사용자가 직접 정의한 예외명을 사용할 수 있다.
- 만약 구체적인 예외명을 알 수 없다면 **OTHERS**를 사용하면 되는데 이렇게 하면 Oracle 시스템에서 PL/SQL 코드 상 발생한 Runtime Exception을 자동으로 잡아준다. 
