## Chapter07 C#  
### (1) C# Lambda 
  ① Lambda  

  ```C#
  delegate int Calculate(int a, int b);
  
  ```
  - Lambda는 Anonymous Method를 만들기 위해서 사용한다.  
  - Lambda로 만드는 Anonymous Method는 Anonymous Functions라는 이름으로 부르는데, 보통 Method의 경우에는 입력값(Parameter)과 출력값(return)을 가지고 있듯이 Lambda역시 동일하다. 
  - C#에서 Lambda가 나오기 전에는 Anonymous Functions라는 개념으로 등장한 것이 바로 Delegate와 Extension Methods 이다.
  - Lambda는 다른 말로 Arrow Function 이러고 한다.   

|종류|형태|예|
|-----|---| ---|
|Lambda Expression|parameter => expression| x=> x+1 |
|Lambda Statement |parameter => statement| x => {return x + 1;}|

```C# 
 
```


  참조   
  > [Lambda](https://docs.microsoft.com/ko-kr/dotnet/csharp/language-reference/operators/lambda-expressions)     
  > [이것이C#이다](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=260230941)     
   

