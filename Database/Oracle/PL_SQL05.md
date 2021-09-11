## Oracle PL_SQL Chapter05
### PL/SQL Cursor
**(1) PL/SQL Cursor** 
- SQL의 가장 큰 특징은 Data를 집합적, 일괄적으로 처리한다는 것이다.  Row를 하나씩 개별적으로 처리하기 보다는 특정 조건에 맞는 Row를 선별해서 한꺼번에 처리한다. 
- Procedure를 개발하다 보면 Data를 한 개의 Row씩 처리해야 하는 상황이 발생하는 데 이때 Cursor를 이용한다. 
- 특정 SQL문을 처리한 결과를 담고 있는 영역(Private memory area)을 가리키는 일종의 Point로, Cursor를 사용하면 처리된 SQL문의 결과 집합에 접근이 가능하다. 
- SQL문은 집합적 언어이므로 임의의 SQL문이 처리된 결과의 Row 수는 한 개 이상인데 Cursor을 사용해 개별 Row에 순차적으로 접근이 가능하다.  
- **Implicit cursor**
  - Oracle 내부에서 자동으로 생성되어 사용하는 Cursor로, SQL문(INSERT, UPDATE, MERGE, DELETE, SELECT INTO)이 실행될 때 마다 자동으로 만들어져서 사용된다. 
  - 개발자의 입장에서는 이러한 Cursor의 동작에 관여할 수는 없지만, Cursor 속성을 이용하면 여러가지 정보를 얻어낼 수 있다. 
- **Explicit cursor**
  - 사용자가 직접 정의해서 사용하는 Cursor을 의미한다. 
- Implicit cursor, Explicit cursor에 관계없이 open - fetch - clse 3단계로 진행된다. 


 
