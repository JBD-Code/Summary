## Chapter09 C#  

### (1) Event   
 - 프로그래밍에서 어떤 행위(Event)가 발생했을 때 이를 외부의 Event 가입자(subscriber)들에게 알려주는 기능을 하는 object가 **Event**이다.
 - Event에 가입하는 외부 가입자 측에서는 Event가 발생했을 대 어떤 명령을 실행할지를 지정해 주는데 이를 **Event Handler** 라고 한다. 
 - Event에 가입하기 위해서는 += 연산자를 사용해 Event Handler을 Event에 추가, 반대의 경우에는 -= 연산자를 사용한다.
 - 하나의 Event에 여러 개의 Event Handler를 추가할 수 있고 추가된 Event Handler를 모두 차례로 호출한다.    
 - Event의 동작원리는 delegate와 유사하다. Event는 delegate를 event 한정자로 수식해서 생성한다. 
   
### (2) Event 생성
   -  Delegate를 선언한다. 이 때 Delegate는 class 밖에 선언해도 되고 안에 선언해도 된다.
   - 위 과정에서 선언한 대리자의 Instance를 class내에서 Event 한정자로 수식해서 선언한다.  
   - Event Handler를 작성한다.  Event Handler는 Delegate와 일치하는 Method면 된다.
   - class의 Instance를 생성하고 이 객체의 Event에 Event 핸들러를 등록한다. 
   - Event가 발생하면 Event Handler을 호출한다.

  참조   
  > [Microsoft Event](https://docs.microsoft.com/ko-kr/dotnet/csharp/language-reference/keywords/event)   
  > [이것이 C#이다](https://www.aladin.co.kr/shop/wproduct.aspx?ItemId=260230941)  
  > [예제로 배우는 C# 프로그래밍](https://www.csharpstudy.com/CSharp/CSharp-event.aspx) 
  
