
## Oracle Query
### Function 

**(1) 문자 함수**
- **INITCAP(char)**
  - 매개변수로 들어오는 char의 첫문자를 대문자로 나머지는 소문자로 반환한다.
  - 첫 문자를 인식하는 기준은 공백과 알파벳(숫자)을 제외한 문자로 공백, 알파벳(숫자)이 아닌 문자를 만난 후 첫 알파벳을 대문자로 변환한다.
```SQL
  SELECT INITCAP('never say goodbye'),
         INITCAP('never 6say*good가bye')
    FROM DUAL;
    //Never Say Goodbye
    //Never 6sayGood가Bye
```

- **LOWER(char), UPPER**
  - LOWER(char)는 매개변수로 들어오는 문자를 모두 소문자로, UPPER(char)는 대문자로 변환한다.   
```SQL
   SELECT LOWER('abcDEF'),
          UPPER('GHIjkl'),
          LOWER('NEVER SAY GOODBYE'),
          UPPER('never say goodbye')
     FROM DUAL;
     // abcdef
     // GHIJKL
     // never say goodbye
     // NEVER SAY GOODBYE
```

- **CONCAT(char1, char2)**
  - CONCAT(char1, char2)은 '||' 연산자 처럼 매개변수로 들어오는 두문자를 연결해서 반환한다. 
```SQL
   SELECT CONCAT('I have' , 'a dream'),
                 'I have' || 'a dream'
     FROM DUAL;

```

- **SUBSTR(char, pos, len)**
  - 문자열 char의 pos번째 문자부터 len 길이만큼 잘라낸 결과를 반환한다.
  - pos 값으로 0이 오면 Default 값인 1, 즉 첫번째 문자를 가리킨다. 음수가 오면 char 문자열 맨 끝에서 시작한 상대적 위치를 의미한다. 
  - len값이 생략되면 pos번째 문자부터 나머지 모든 문자를 반환한다. 
```SQL
   SELECT SUBSTR('ABCDEFG', 1, 4),
          SUBSTR('ABCDEFG', -2, 2),
          SUBSTR('가나다라마바사', 1),
          SUBSTR('가나다라마바사', -3, 3)
     FROM DUAL;
     // ABCD
     // FG
     // 가나다라마바사
     // 마바사 

```

- **SUBSTRB(char, pos, len)**
  - 문자 개수가 아닌 문자열의 Byte 수만큼 잘라낸 결과를 반환한다. 
```SQL
   SELECT SUBSTRB('ABCDEFG', 1, 4),
          SUBSTRB('ABCDEFG', -2, 2),
          SUBSTRB('가나다라마바사', 1),
          SUBSTRB('가나다라마바사', -3, 3)
     FROM DUAL;
     // ABCD
     // FG
     // 가나다라마바사
     // 사
```
- **LTRIM(char, set), RTRIM(char, set)**
  - 매개변수로 들어온 char 문자열에서 set으로 지정된 문자열을 좌우 끝에서 제거한 후에 결과를 반환한다. 
  - set는 생략이 가능하며 Default로 공백 문자 한글자가 사용된다. 
  - set에 명시된 문자를 한 번씩만 제거하며, set 문자로 명시한 문자가 좌우 끝에 없을 때 문자열 전체를 반환한다. 
```SQL
   SELECT LTRIM('ABCDEFGABC', 'ABC'),
          RTRIM('ABCDEFGABC', 'ABC'),
          LTRIM('가나다라마바사', '가'),
          RTRIM('가나다라마바사', '가')
     FROM DUAL;
     // DEFGABC
     // ABCDEFG
     // 나다라마바사
     // 가나다라마바사
 ```
- **LPAD(expr1, n, expr2), RPAD(expr1, n, expr2)**
  - 매개변수로 들어온 expr2 문자열을 n자리 만큼 좌우부터 채워 expr1을 반환한다. 
  - 매개변수 n은 expr2, expr1이 합쳐져 반환되는 총 자릿수를 의미한다. 
  - 매개변수 expr2 문자열을 생략할 경우 Default로 공백 한 문자가 사용된다.  
 ```SQL
    CREATE TABLE EX4_1 (PHONE_NUM VARCHAR(30));
 
    INSERT INTO EX4_1 VALUES('111-1111');
    INSERT INTO EX4_1 VALUES('111-2222');
    INSERT INTO EX4_1 VALUES('333-3333');

   SELECT RPAD(PHONE_NUM, 12, '(02)')
     FROM EX4_1;
     //111-1111(02)
     //111-2222(02)
     //333-3333(02)
```

- **REPLACE(char, search_str, replace_str)**
  - char 문자열에서 sear 문자열을 찾아서 이를 replace_st r문자열로 대체한 결과를 반환한다.  
  - LTRIM, RTRIM을 사용해서 좌우 끝의 공백을 제거할 수 있지만 중간에 있는 공백을 제거할 수 없다. 하지만 REPLACE를 사용하면 가능하다.
```SQL
   SELECT REPLACE('CODE NAME IS JAVA KILLER!', 'JAVA', 'C#')
     FROM DUAL;
     //CODE NAME IS C# KILLER!
```
```SQL
 SELECT RTRIM('  ABD  DEF '),
        LTRIM('  ABD  DEF '),
        REPLACE('  ABD  DEF  ', ' ', '')
   FROM DUAL;
   //  ABD  DEF	
   //ABD  DEF 	
   //ABDDEF
```

- **INSTR(str, substr, pos, occur)**
  - str문자열에서 substr과 일치하는 위치를 반환하는데, pos는 시작 위치로 Default 값은 1, occur은 몇 번째 일치하는지를 명시하며 Default 값은 1이다. 
 ```SQL 
 SELECT INSTR('내가 만약 즐거울 때면, 내가 만약 괴로울 때면, 내가 만약 외로울 때면', '만약'),
        INSTR('내가 만약 즐거울 때면, 내가 만약 괴로울 때면, 내가 만약 외로울 때면', '만약', 5),
        INSTR('내가 만약 즐거울 때면, 내가 만약 괴로울 때면, 내가 만약 외로울 때면', '만약', 5, 2),
   FROM DUAL;
   //4
   //8
   //32
 ``` 
- **LENGTH(char), LENGTHB(char)**
  - LENGTH는 매개변수로 들어온 문자열의 개수를 반환하고, LENGTHB는 매개변수로 들어온 문자열의 Byte를 반환한다. 
```SQL 
   SELECT LENGTH('프로그래머'),
          LENGTHB('프로그래머'),
          LENGTH('programmer'),
          LENGTHB('programmer')
     FROM DUAL;
     //5
     //15
     //10
     //10
```
