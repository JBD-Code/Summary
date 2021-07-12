
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
