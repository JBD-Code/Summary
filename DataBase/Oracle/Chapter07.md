
## Oracle Query
### Function 

**(1) 문자 함수**
- **INITCAP(char)**
  - 매개변수로 들어오는 char의 첫문자를 대문자로 나머지는 소문자로 반환한다.
  - 첫 문자를 인식하는 기준은 공백과 알파벳(숫자)을 제외한 문자 즉 공백, 알파벳(숫자)이 아닌 문자를 만난 후 첫 알파벳을 대문자로 변환한다.
```SQL
  SELECT INITCAP('never say goodbye'),
         INITCAP('never 6say*good가bye')
    FROM DUAL;
    //Never Say Goodbye
    //Never 6sayGood가Bye
```
-**LOWER(char), UPPER**
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
-**CONCAT(char1, char2)
  - CONCAT(char1, char2)은 '||' 연산자 처럼 매개변수로 들어오는 두문자를 연결해서 반환한다. 
```SQL
   SELECT CONCAT('I have' , 'a dream'),
                 'I have' || 'a dream'
     FROM DUAL;

```
-**SUBSTR(char, pos, len)
  - 잘라올 문자열인 char의 pos번째 문자부터 len 길이만큼 잘라낸 결과를 반환한다.
  - pos 값으로 0이 오면 Default 값인 1, 즉 첫번째 문자를 가리킨다. 음수가 오면 char 문자열 맨 끝에서 시작한 상대적 위츠를 의미한다. 
  - len값이 생략되면 pos번째 문자부터 나머지 모든 문자를 반환한다. 
 
```SQL
   SELECT SUBSTR('ABCDEFG', 1, 4),
   		    SUBSTR('ABCDEFG', -1, 4),
   		    SUBSTR('ABCDEFG', 1),
   		    SUBSTR('ABCDEFG', -1)
   	 FROM DUAL;
     // ABCD
     // G
     // ABCDEFG
     // G

```

-**SUBSTRB(char, pos, len)
  - CONCAT(char1, char2)은 '||' 연산자 처럼 매개변수로 들어오는 두문자를 연결해서 반환한다. 
```SQL
   SELECT SUBSTR('ABCDEFG', 1, 4),
   		    SUBSTR('ABCDEFG', -1, 4),
   		    SUBSTR('ABCDEFG', 1),
   		    SUBSTR('ABCDEFG', -1)
   	 FROM DUAL;
     // ABCD
     // G
     // ABCDEFG
     // G

```




