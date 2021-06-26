## Oracle Query
### User

#### (1) CREATE

```SQL
   CREATE USER scott 
   IDENTIFIED BY tiger
``` 

#### (2) ALTER 
```SQL
  //LOCK 
   ALTER USER scott 
   ACCOUNT UNLOCK
     
  //UNLOCK 
   ALTER USER scott 
   ACCOUNT LOCK
     
  //Unlock and create new password  
   ALTER USER scott 
   IDENTIFIED BY tiger  
   ACCOUNT UNLOCK
```

#### (3) GRANT 
```SQL
   GRANT CONNECT, 
         RESOURCE,
         DBA TO scott
   
   GRANT CREATE SESSION
      TO scott
   
   GRANT CREATE TABLE 
      TO scott 
   
   GRANT DROP ANY TABLE 
      TO scott 
```

