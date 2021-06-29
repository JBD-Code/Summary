
## Oracle Summary 00 
### DataBase Object 
**(1) Database Object** 
- Database Object란 Database내에 존재하는 논리적인 저장 구조를 말한다. 
- DBMS가 Data를 관리하려면 Data를 어딘가에 저장해서 관리해야 하는데 이런 목적을 달성하기 위한 모든 논리적인 저장 구조가 Database Object이다. 

**(2) Table**

- Data를 입력, 수정, 삭제하는 즉 Data를 담고 있는 Object
- Table는 DBMS에서 가장 기본적인 Object로 Row , Cloumn으로 구성된 2차원의 형태이다.
- Table name, Column name은 최대 30byte 가능하다.
- Table name, Column name은 예약어 사용이 불가능하다.
- Table name, Column name은 문자, 숫자, '_', '$', '#'을 사용가능하지만 첫 글자는 문자만 올수 있다.
- 하나의 Table에 사용 가능한 Column은 최대  255개이다.   

**(3) View** 

- View 는 하나 이상의 Table이나 다른 View 를 볼 수 있게 하는 Database Object이다.  
- 실제 데이터는 View 를 구성하는 Table에 담겨 있지만 마치 Table처럼 사용할 수 있다.
- Table뿐만 아니라 다른 View 를 참조해서 새로운 View를 만들 수 있다. Data를 본다는 의미가 있으므로 View의 정의는 데이터를 조회하는 SELECT 문으로 구성된다.
- 현장에서는 여러 개의 테이블에서 필요한 정보를 뽑아 사용할 때가 많은데 이때 선택할 수 있는 최선책이 View이다. 
- View는 데이터 보안 측면에서 유리하며, View를 보면 Column과 Data만 공개가 되므로 원천 Table을 감출 수 있다. 
- View는 다른 Table를 참조하고 있으므로 View를 삭제하더라도 실제의 Data는 삭제되지 않는다. 또한 기존에 생성된 View를 수정하는 구문은 View생성 Query와 동일하다. 
- CREATE OR Replace가 생성 혹은 대체한다는 의미 이므로 이 구문을 사용해서 View의 정의 부분을 수정 View 가 가져오는 원천테이블이나 Column을 변경할 수 있다.
- View는 읽기 전용 View 와 Data 수정 가능한 View가 존재한다.

```SQL
   SELECT a.EMPLOYEE_ID, 
          a.EMP_NAME, 
          a.DEPARTMENT_ID,
          b.DEPARTMENT_NAME     
     FROM EMPLOYEES a,
          DEPARTMENTS  b
    WHERE a.DEPARTMENT_ID  = b.DEPARTMENT_ID;
```
- 위와 같이 자주 사용되는 정보를 아래와 같은 View로 생성이 가능하다. 

```SQL
  CREATE OR REPLACE VIEW EMP_DEPT_V1 AS 
  SELECT A.EMPLOYEE_ID, 
         A.EMP_NAME, 
         A.DEPARTMENT_ID,
         B.DEPARTMENT_NAME
    FROM EMPLOYEES A,
         DEPARTMENTS B
   WHERE A.DEPARTMENT_ID = B.DEPARTMENT_ID;
```

**(4) Index**
- Index는 Table에 있는 Data를 빨리 찾기 위한 용도의 Database Object이다. 
- 특성에 따른 Index의 분류 
   - Index 구성 Column 개수에 따른 분류 : Single Index, Composite Index
   - 유일성에 여부에 따른 분류 : Unique Index, Non-Unique Index 
   - Index 내부 구조에 따른 분류 : B-tree Index, Bitmap Index, Function Based Index
- Index는 Table에 존재하는 한 개 이상의 Column으로 만들 수 있다. 
- B-tree Index는 Index-Key와 이 Key에 해당하는 Column 값을 가진 Table의 Row가 저장된 주소값으로 구성된다. 

```SQL
   CREATE UNIQUE INDEX EX2_5_IX01
       ON EX2_5(COLUMN3);
```

```SQL
   SELECT INDEX_NAME, INDEX_TYPE, TABLE_NAME, UNIQUENESS
     FROM USER_INDEXES
    WHERE TABLE_NAME = 'EX2_5';
```
```SQL
   DROP INDEX EX2_5_IX01;
```


**(5) Synonym**
- 'Synonym'은 '동의어'란 의미로 Database object에는 각자 고유한 이름이 있는 데 이 object에 대한 동의어를 만드는 것이 바로 Synonym이다. 
- Public Synonym와 Private Synonym가 있으며 Public Synonym은 모든 user이 접근 가능하지만 Private Synonym은 특정 user만 접근이 가능하다. 
-
