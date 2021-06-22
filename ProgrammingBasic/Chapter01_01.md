## Chapter01 C#  
### (1) C# Delegate    
  ① Delegate의 선언 

  ```C#
    private delegate int RunCalc(int a, int b);
  
    //한정자 delegate 반환 형식 대리자이름 ( 매개변수 );
  ```
  - RunCalc 라는 Delegate 선언의 경우 속이 비어있고, 정수형 변수 a, b를 매개변수로 받는 Method 형식이다. 
  - 매개변수가 없는 Delegate 선언도 가능하다.

  ```C# 
  
  class delegateTest01
      {
          private delegate int RunCalc(int a, int b);

          private static int LF_Sum(int p_num1, int p_num2)
          {
              return p_num1 + p_num2;
          }

          private static int LF_Mul(int p_num1, int p_num2)
          {
              return p_num1 * p_num2;
          }

          static void Main(string[] args)
          {
              RunCalc runSum = LF_Sum;
              RunCalc runMul = LF_Mul;
              Console.WriteLine(runSum(1, 4));
              Console.WriteLine(runMul(3, 5));
          }
      }
  ```
  
  - **LF_Sum(), LF_Mul()** Method를 구현하고 **Runcalc**의 선언은 **LF_Sum(), LF_Mul()** 처럼 두 개의 매개변수를 입력받고 있다.
  - Delegate는 Method에 대한 참조이다. Delegate에 Method의 주소를 할당한 후 Delegate를 호출하면 RunCalc가 LF_Sum(), LF_Mul() Method를 호출해 준다.
  - Delegate의 선언은 반환 형식, 매개변수는 할당되는 Method와 같은 형태를 가지고 있어야 하며 다른 형태를 가지고 있을 경우에는 할당되지 않는다.

② Delegate의 활용 

- 별도로 Method를 만들지 않고 한번 사용하면 불필요해지는 기능을 만들 경우에 유용하게 사용된다.
- "값"이 아닌 "코드" 자체를 매개변수로 넘기고 싶을 때 사용한다. 

### (2) C# Delegate Chaining     
① Delegate Chaining
  - Delegate Chaining이란 하나의 Delegate를 이용해서 여러 개의 Method를 호출 할 수 있다.

```C#
class delegateTest02
    {
        private delegate void ThereisFire(string location);

        private static void LF_Call(string p_sLocation)
        {
            Console.WriteLine($"{p_sLocation}");
        }

        private static void LF_ShotOut(string p_sLocation)
        {
            Console.WriteLine($"{p_sLocation}");
        }

        private static void LF_Escape(string p_sLocation)
        {
            Console.WriteLine($"{p_sLocation}");
        }

        static void Main(string[] args)
        {
            ThereisFire fire= new ThereisFire(LF_Call)
             + new ThereisFire(LF_ShotOut)
             + new ThereisFire(LF_Escape);

            fire("SuperMarket");
            Console.ReadLine();
        }
    }
```
② Delagete.Combine Method 

```C#
class delegateTest03
{
		private delegate void RunCalc(int a, int b);

    private static void LF_Sum(int p_num1, int p_num2)
    {
        Console.WriteLine($"{p_num1} + {p_num2} = {p_num1 + p_num2}");
    }

    private static void LF_Mul(int p_num1, int p_num2)
    {
        Console.WriteLine($"{p_num1} * {p_num2} = {p_num1 * p_num2}");
    }

    private static void LF_Div(int p_num1, int p_num2)
    {
        Console.WriteLine($"{p_num1} / {p_num2} = {p_num1 / p_num2}");

    }

    static void Main(string[] args)
    {
        RunCalc calc = (RunCalc)Delegate.Combine(new RunCalc(LF_Sum),
                                                 new RunCalc(LF_Mul),
                                                 new RunCalc(LF_Div));

        calc(20, 4);
        Console.ReadLine();
    }
}
```
④  

⑤
  
⑥ 



  참조   
  > [Delegate](https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/delegates/)     
   

