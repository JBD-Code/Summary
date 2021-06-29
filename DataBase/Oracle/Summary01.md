
## Oracle Summary 00 
### DataBase Object 

**(1) Database Object** 
- Database Object란 Database내에 존재하는 논리적인 저장 구조를 말한다. 
- DBMS가 Data를 관리하려면 Data를 어딘가에 저장해서 관리해야 하는데 이런 목적을 달성하기 위한 모든 논리적인 저장 구조가 Database Object이다. 

**(2) Table**
- Data를 입력, 수정, 삭제하는 즉 Data를 담고 있는 
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
- CREATE OR REPLACE가 생성 혹은 대체한다는 의미이므로 이 구문을 사용해서 View의 정의 부분을 수정 View 가 가져오는 기존 Table, Column을 변경할 수 있다.
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

- 'Synonym'은 동의어란 의미로 Database Object에는 각자 고유한 이름이 있는데 이 Object에 대한 동의어를 만드는 것이 바로 Synonym이다. 
- Public Synonym은 모든 user가 접근 가능하고, Private Synonym은 특정 user만 접근 가능하다. 
- Database의 투명성을 위해서 사용하며, 다른 사용자의 객체를 많이 참조할 때 사용된다.
- Synonym 생성후 이 Synonym을 참조하고 있는 Object의 이름이 변경 되더라도 이전에 작성한 Query를 수정할 필요가 없다. 
- Synonym은 별칭이므로 기존 Object를 숨길 수 있기 때문에 보안 측면에 유리하다. 

```SQL
   CREATE OR REPLACE SYNONYM SYN_CHANNEL
      FOR CHANNELS;
```
```SQL
   SELECT COUNT(*)
     FROM SYN_CHANNEL
```
```SQL
   SELECT COUNT(*)
     FROM CHANNELS ;
```
```SQL
   DROP SYSNONYM SYN_CHANNEL;
```

**(6) Sequence**

- Sequence는 자동 순번을 반환하는 Database Object이다. 
- 단순히 증감 연산을 사용해서 유일한 숫자를 구할 때 Sequence를 사용하면 유리하다. 
  - INCREMENT BY 증감숫자 : 증감 숫자는 0이 아닌 정수로 양수인 경우 증가 음수인 경우에는 감소한다. 
  - START WITH 시작숫자 : 시작 숫자의 DEFAULT 값은 증가일 경우 MINVALUE, 감소일 경우에는 MAXVALUE
  - NOMINVALUE : DEFAULT 값으로 증가의 경우 1, 감소의 경우 -(1027-1) 
  - MINVALUE 최소값 : 최소값은 시작 숫자와 작거나 같아야 하고 MAXVALUE 보다 작아야 한다. 
  - NOMAXVAULE : DEFAULT 값으로 증가의 경우 1028-1, 감소의 경우 -1
  - MAXVALUE 최대값 : 최대값은 시작 숫자와 같거나 커야 하고 MINVALUE 보다 작아야 한다. 
  - NOCYCLE : DAFALUR 값으로 최대값 , 최소값에 도달하면 생성을 중지한다.
  - CYCLE : 증가는 최대값에 도달하면 다시 최소값부터 시작, 감소는 최소값에 도달하면 다시 최대값에서 시작한다.  
  - NOCACHE : DEFAULT로 Memory에 Sequence값을 미리 할당해 놓지 않고 DEFAULT 값은 20
  - CACHE : MEMORY에 Sequence값을 미리 할당해 놓는다.  

```SQL
   CREATE SEQUENCE MY_SEQUENCE_1 
   INCREMENT BY 1 
   START WITH 1
   MINVALUE 1
   MAXVALUE 1000
   NOCYCLE
   NOCACHE;
```

```SQL
   INSERT INTO EX2_4 (COL1) VALUES (MY_SEQUENCE_1.NEXTVAL);
```
- SEQUENCE Name.NEXTVAL을 사용하면 해당 Sequence에서 다음 순번을 자동으로 가져온다.
- SEQUENCE Name.NEXTVAL을 사용하면 값이 계속 증가한다. INSERT문이 아니라 SELECT 문을 사용해도 값이 증가한다 

```SQL
   SELECT MY_SEQUENCE_1.NEXTVAL
     FROM DUAL;
```
- SEQUENCE Name.CURRVAL을 사용하면 해당 Sequence의 현재 값을 알 수 있다. 

```SQL
   SELECT MY_SEQUENCE_1.CURRVAL
     FROM DUAL; 
```


```SQL
   DROP SEQUENCE MY_SEQUENCE_1;
```
