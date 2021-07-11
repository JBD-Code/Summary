
## Oracle Query
### Function 

**(1) 숫자 함수**
- **ABS(n)**
  - 매개변수로 숫자를 받아 그 절대값을 반환한다.
```SQL
   SELECT ABS(10), 
          ABS(-34234),
          ABS(-10.343)
     FROM DUAL;
     
     //10
     //34234
     //10.343
```
- **CEIL(n)**
  - 매개변수 n과 같거나 가장 큰 정수를 반환한다. 
```SQL
   SELECT CEIL(10.123),
          CEIL(10.343),
          CEIL(11.001),
          CEIL(12),
          CEIL(-323)
     FROM DUAL;

     //11
     //11
     //12
     //12
     //-323
```
- **FLOOR(n)** 
  - 매개변수 n보다 작거나 가장 큰 정수를 반환한다. 
```SQL
   SELECT FLOOR(10.123),
          FLOOR(10.345),
          FLOOR(11.001),
          FLOOR(12),
          FLOOR(-344)
     FROM DUAL;
```
- **ROUND(n, i)**
  - 매개변수 n을 소수점 기준 (i+1)번 째에서 반올림한 결과를 반환한다. 
  - i는 생략할 수 있고 Default 값은 0이다. 
  - i가 음수이면 소수점 기준으로 왼쪽 i번째에서 반올림이 일어난다.
```SQL
   SELECT ROUND(10.153),
          ROUND(10.345),
          ROUND(10.553),
          ROUND(12),
          ROUND(-34.75)
    FROM DUAL; 
     //10
     //10
     //11
     //-35
```
```SQL
   SELECT ROUND(10.153, 1),
          ROUND(10.345, 1),
          ROUND(10.553, 1),
          ROUND(12, 1),
          ROUND(-34.75, 1)
     FROM DUAL; 
     //10.2
     //10.3
     //10.6
     //12
     //-34.8
```
```SQL
   SELECT ROUND(0, -1),
          ROUND(10.345, -1),
          ROUND(15.553, -1),
          ROUND(57, -2),
          ROUND(-54.75, -2)
     FROM DUAL; 
     //0
     //10
     //20
     //100
     //-100
```
- **TRUNC(n1, n2)** 
  -  반올림하지 않고 n1을 소수점 기준 n2 자리에서 무조건 잘라낸 결과를 반환한다 
  -  n2는 생략할 수 있으며 Default 값은 0이다. 
  -  양수일 경우에는 소수점 기준 오른쪽으로, 음수일 경우에는 소수점 기준 왼쪽 자리에서 잘라낸다. 
```SQL
   SELECT TRUNC(10.153),
          TRUNC(10.345),
          TRUNC(10.5534),
          TRUNC(12),
          TRUNC(-234.75)
     FROM DUAL;
     //10
     //10
     //10
     //12
     //-234
```

```SQL
   SELECT TRUNC(10.153, 1),
          TRUNC(10.345, 2),
          TRUNC(10.5534, 3),
          TRUNC(12, -1),
          TRUNC(-234.75, -2)
     FROM DUAL; 
     //10.1
     //10.34
     //10.553
     //10
     //-200
```
 - **POWER(n2, n1)** 
    - 매개변수 n2를 n1제곱한 결과를 반환한다. 
    - n1에는 정수와 실수가 모두 올 수 있지만, 만약 n2가 음수일 경우에는 n1은 정수만 올 수 있다. 
```SQL
   SELECT POWER(3, 2),
          POWER(4, 1),
          POWER(5, 3),
          POWER(12.5, 2),
          POWER(4, 3.3)
     FROM DUAL;
     //9
     //4
     //125
     //156.25
     //97.00586025666547727022462728361249527181
```
```SQL
   SELECT POWER(-3, 3),
       	  POWER(-3, 2)
     FROM DUAL;
     //-27
     //9
```
```SQL
   SELECT POWER(-3, 0.2)
     FROM DAUL;
     //SQL Error ORA-00942
```
- **SQRT(n)**
  - n의 제곱근을 반환한다. 
```SQL
   SELECT SQRT(2),
          SQRT(3),
          SQRT(4),
          SQRT(9)
     FROM DUAL;
     //1.41421356237309504880168872420969807857
     //1.73205080756887729352744634150587236694
     //2
     //3
```
- **MOD(n2, n1)**
  - n2 를 n1으로 나눈 나머지 값을 반환한다. 
 ```SQL
 
    SELECT MOD(7.7, 3),
           MOD(-5, 2),
           MOD(3.3, 2),
           MOD(2.135, 3)
      FROM DUAL;
      //1.7
      //-1
      //0
      //1.3
      //2.135
 ```
- **REMAINDER(n2, n1)** 
  - n2를 n1으로 나눈 나머지 값을 반환한다. 나머지를 구하는 연산방법이 MOD 함수와 다르다.  
  - MOD 함수의 경우 MOD n2 -n1 * **FLOOR(n2/n1)**
  - REMAINDER 함수의 경우 n2-n1 * **ROUND(n2/n1)**

```SQL
   SELECT REMAINDER(7.7, 3),
          REMAINDER(-5, 2),
          REMAINDER(3.3, 2),
          REMAINDER(2.134, 3)
     FROM DUAL;
     //-1.3
     //-1
     //-0.7
     //-0.866   
```


**(2) 문자 함수**
①
②
③
④
⑤
⑥


**(3) 날짜 함수**
①
②
③
④
⑤
⑥

**(4) 변환 함수**
①
②
③


**(5) NULL 함수**
①
②
③
④

**(5) 기타 함수**
①
②
