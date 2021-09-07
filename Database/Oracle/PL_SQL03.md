## Oracle PL_SQL Chapter03
### PL/SQL User Defined Exception
**(1) PL/SQL User Defined Exception** 
- Oracle에서는 사용자가 직접 예외를 정의해서 사용할 수 있다. 
- 사용자 정의 예외를 사용하려면 변수, 상수처럼 PL/SQL 블록의 선언부에서 예외를 정의해야한다. 
- 시스템 예외는 자동으로 검출되지만, 사용자 예외는 직접 예외를 발생시켜야 하는데 "RAISE 예외명" 형태로 사용한다. 
- 예외를 발생 시키면 자동으로 제어권이  EXCEPTION 절로 넘어오므로 시스템예외와 동일한 방식으로 처리해주면 된다. 
 
