## Oracle PL_SQL Chapter04
### PL/SQL Transaction
**(1) PL/SQL Transaction** 
- Database의 특정 Table에서 Data를 읽어 조작 후 다른 Table에 Data를 입력, 생신 삭제 하는데 처리 도중에 오류가 발생하면 모든 작업을 원상태로 돌리고, 처리과정이 모두 성공했을 때만 Database에 반영하는 것이 Transaction 처리이다.    

**(2) COMMIT , ROLLBACK**
- **COMMIT** 
  - 모든 처리과정을 성공적으로 마쳤을 때 결과를 반영해도 된다는 역할을 하는 것이 바로 COMMIT문이다. 
  - COMMIT문을 실행하지 않으면 INSERT, UPDATE, DELETE, MERGE한 결과가 최종적으로 Table에 반영되지 않는다. 
 ```SQL
 COMMIT[WORK]
 ```

 
